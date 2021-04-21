<template>
  <div id="app" style="padding-top: 118px">
    <div
      class="field has-background-white"
      style="position: fixed; top: 0; z-index: 1; width: 100vw"
    >
      <div class="control">
        <input
          class="input is-large"
          type="text"
          v-model="seatchText"
          placeholder="検索ワード"
        />
      </div>
      <div class="control">
        <label class="checkbox">
          <input type="checkbox" v-model="filterType.identify" />
          ジョブ特性
        </label>
        <label class="checkbox">
          <input type="checkbox" v-model="filterType.ability" />
          サブアビリティ
        </label>
        <label class="checkbox">
          <input type="checkbox" v-model="filterType.head" />
          頭装備
        </label>
        <label class="checkbox">
          <input type="checkbox" v-model="filterType.body" />
          体装備
        </label>
        <label class="checkbox">
          <input type="checkbox" v-model="filterType.shield" />
          盾
        </label>
        <label class="checkbox">
          <input type="checkbox" v-model="filterType.weapon" />
          武器
        </label>
        <label class="checkbox">
          <input type="checkbox" v-model="filterType.accessory" />
          アクセサリー
        </label>
      </div>
    </div>
    <template v-for="item in filterData" :item="item">
      <identify-card
        :item="item"
        v-if="hasProperty(item, ['name', 'text', 'jobName'])"
        :key="item.name"
      />
      <ability-card
        :item="item"
        v-if="hasProperty(item, ['level', 'name', 'cost', 'effect', 'jobName'])"
        :key="item.name"
      />
      <shield-card
        :item="item"
        v-if="
          hasProperty(item, [
            'name',
            'defence',
            'magician',
            'specialEffects',
            'position',
            'url',
          ])
        "
        :key="item.name"
      />
      <weapon-card
        :item="item"
        v-if="
          hasProperty(item, [
            'name',
            'defence',
            'magician',
            'specialEffects',
            'position',
            'bothHands',
            'type',
            'url',
          ])
        "
        :key="item.name"
      />
      <head-body-card
        :item="item"
        v-if="
          hasProperty(item, [
            'name',
            'defence',
            'magician',
            'specialEffects',
            'position',
            'type',
            'url',
          ])
        "
        :key="item.name"
      />
      <accessori-card
        :item="item"
        v-if="hasProperty(item, ['name', 'effect', 'positon', 'url'])"
        :key="item.name"
      />
    </template>
  </div>
</template>

<script>
import database from "./database.json";
import AbilityCard from "./components/AbilityCard";
import AccessoriCard from "./components/AccessoriCard.vue";
import HeadBodyCard from "./components/HeadBodyCard.vue";
import IdentifyCard from "./components/IdentifyCard.vue";
import ShieldCard from "./components/ShieldCard.vue";
import WeaponCard from "./components/WeaponCard.vue";

export default {
  components: {
    IdentifyCard,
    AbilityCard,
    ShieldCard,
    WeaponCard,
    HeadBodyCard,
    AccessoriCard,
  },
  name: "App",
  data() {
    return {
      seatchText: "",
      filterType: {
        identify: true,
        ability: true,
        shield: true,
        weapon: true,
        head: true,
        body: true,
        accessory: true,
      },
      data: [].concat(
        database.jobList.flatMap((job) =>
          job.identityList.map((identify) =>
            Object.assign({ jobName: job.name }, identify)
          )
        ),
        database.jobList.flatMap((job) =>
          job.abilityList
            .filter((ability) => ability.cost.includes("Cost"))
            .map((ability) => Object.assign({ jobName: job.name }, ability))
        ),
        database.shieldList,
        database.weaponList,
        ...database.headList,
        ...database.bodyList,
        ...database.accessoriesList
      ),
    };
  },
  methods: {
    hasProperty(item, propertyNames) {
      return (
        JSON.stringify(Object.keys(item).sort()) ===
        JSON.stringify(propertyNames.sort())
      );
    },
  },
  computed: {
    filterData() {
      return this.data
        .filter((item) => {
          if (item.text) {
            return item.text.includes(this.seatchText);
          }

          if (item.effect) {
            return item.effect.includes(this.seatchText);
          }

          if (item.specialEffects) {
            return item.specialEffects.includes(this.seatchText);
          }

          return false;
        })
        .filter((item) => {
          if (this.filterType.identify) {
            return this.hasProperty(item, ["name", "text", "jobName"]);
          } else if (this.filterType.ability) {
            return this.hasProperty(item, [
              "level",
              "name",
              "cost",
              "effect",
              "jobName",
            ]);
          } else if (this.filterType.shield) {
            return this.hasProperty(item, [
              "name",
              "defence",
              "magician",
              "specialEffects",
              "position",
              "url",
            ]);
          }
          if (this.filterType.weapon) {
            return this.hasProperty(item, [
              "name",
              "defence",
              "magician",
              "specialEffects",
              "position",
              "bothHands",
              "type",
              "url",
            ]);
          } else if (this.filterType.head) {
            return (
              this.hasProperty(item, [
                "name",
                "defence",
                "magician",
                "specialEffects",
                "position",
                "type",
                "url",
              ]) && item.position === "頭"
            );
          } else if (this.filterType.body) {
            return (
              this.hasProperty(item, [
                "name",
                "defence",
                "magician",
                "specialEffects",
                "position",
                "type",
                "url",
              ]) && item.position === "体"
            );
          } else if (this.filterType.accessory) {
            return this.hasProperty(item, ["name", "effect", "positon", "url"]);
          } else {
            return true;
          }
        });
    },
  },
};
</script>

<style>
.card {
  margin-bottom: 16px;
  width: 1000px;
  border: solid 2px;
}
.checkbox {
  margin-right: 8px;
}
</style>
