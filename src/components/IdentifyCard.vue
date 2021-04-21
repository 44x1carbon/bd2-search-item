<template>
  <div class="card">
    <header class="card-header">
      <p class="card-header-title is-size-4">
        <span class="tag is-medium is-info">ジョブ特性</span>
        <span style="width: 16px"></span>
        {{ item.name }}
      </p>
    </header>

    <table class="table card-content is-fullwidth">
      <tr>
        <th>ジョブ</th>
        <th>効果</th>
      </tr>
      <tr>
        <td>{{ item.jobName }}</td>
        <td>{{ item.text }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: ["item"],
};
</script>