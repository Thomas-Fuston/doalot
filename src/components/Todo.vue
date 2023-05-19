<script>
 export default {
   props: ['todo']
 }
</script>

<template>
    <div class="task" :class="{ 'task-done' : todo.done }" @click.self="$emit('done', todo.id)">
      {{todo.task}}
      <div class="task-actions">
        <span class="task-delete" @click="$emit('delete', todo.id)">
          <i class="ph-trash"></i>
        </span>
      </div>
    </div>
</template>

<style>
.task{
  border: 1px solid #1f2d3d;
  background: #eff2f7;
  margin: 15px 0px;
  padding: 10px 20px;
  display:flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s ease;
  width: 400px;
  box-sizing: border-box;
  cursor: pointer;
}
.task-done{
  background: #29EB7F;
  text-decoration: line-through;
}
.task-delete{
  cursor: pointer;
  text-decoration: none;
}
.task-delete:hover{
  color: #e13314;
}
</style>
