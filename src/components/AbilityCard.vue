<template>
  <div class="card">
    <header class="card-header">
      <p class="card-header-title is-size-4">
        <span class="tag is-medium is-info">サブアビリティ</span>
        <span style="width: 16px"></span>
        {{ item.name }}
      </p>
    </header>

    <table class="table card-content is-fullwidth">
      <tr>
        <th>ジョブ</th>
        <th>レベル</th>
        <th>コスト</th>
        <th>効果</th>
      </tr>
      <tr>
        <td>{{ item.jobName }}</td>
        <td>{{ item.level }}</td>
        <td>{{ item.cost }}</td>
        <td>{{ item.effect }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: ["item"],
};
</script>