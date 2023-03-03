<template>
  <form>
    <div class="form-control">
      <label>Task</label>
      <input type="text" name="text" placeholder="Add Task">
    </div>
    
    <div class="form-control">
      <label>Date & Time</label>
      <input type="text" name="date" placeholder="March 24 at 3:00am">
    </div>

    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="check-box" name="reminder">
    </div>

    <input type="submit" value="Save Task" class="btn btn-block">
  </form>
</template>

<script>
export default {
    name: "AddTask",
}
</script>

<style>

</style>