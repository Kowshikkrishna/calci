<script>
  export let value = 0;
  export let action;
</script>
<style>
  .btn {
    position: relative;
    color: #393a42;
    color: #fff;
    background-color: #9edaf9;
  }

</style>
<button
  class="btn "
  {value}
  on:click={e => action(e.target.value)}>
  {value}
</button>