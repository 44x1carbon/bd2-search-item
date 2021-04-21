<template>
  <div>
    <identify-card
      :item="item"
      v-if="hasProperty(['name', 'text', 'jobName'])"
    />
    <ability-card
      :item="item"
      v-if="hasProperty(['level', 'name', 'cost', 'effect'])"
    />
    <shield-card
      :item="item"
      v-if="
        hasProperty([
          'name',
          'defence',
          'magician',
          'specialEffects',
          'position',
        ])
      "
    />
    <weapon-card
      :item="item"
      v-if="
        hasProperty([
          'name',
          'defence',
          'magician',
          'specialEffects',
          'position',
          'bothHands',
          'type',
        ])
      "
    />
    <head-body-card
      :item="item"
      v-if="
        hasProperty([
          'name',
          'defence',
          'magician',
          'specialEffects',
          'position',
          'type',
        ])
      "
    />
    <accessori-card
      :item="item"
      v-if="hasProperty(['name', 'effect', 'positon'])"
    />
  </div>
</template>

<script>
import AbilityCard from "./AbilityCard.vue";
import AccessoriCard from "./AccessoriCard.vue";
import HeadBodyCard from "./HeadBodyCard.vue";
import IdentifyCard from "./IdentifyCard.vue";
import ShieldCard from "./ShieldCard.vue";
import WeaponCard from "./WeaponCard.vue";
export default {
  components: {
    IdentifyCard,
    AbilityCard,
    ShieldCard,
    WeaponCard,
    HeadBodyCard,
    AccessoriCard,
  },
  props: ["item"],
  methods: {
    hasProperty(item, propertyNames) {
      return (
        JSON.stringify(Object.keys(item).sort()) ===
        JSON.stringify(propertyNames.sort())
      );
    },
  },
};
</script>