<template>
  <div class="card">
    <header class="card-header">
      <p class="card-header-title is-size-4">
        <span class="tag is-medium is-info">{{ item.position }}</span>
        <span style="width: 16px"></span>
        <a :href="item.url" target="_brank">{{ item.name }}</a>
      </p>
    </header>

    <table class="table card-content is-fullwidth">
      <tr>
        <th>物防</th>
        <th>魔防</th>
        <th>効果</th>
      </tr>
      <tr>
        <td>{{ item.defence }}</td>
        <td>{{ item.magician }}</td>
        <td>{{ item.specialEffects }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: ["item"],
};
</script>