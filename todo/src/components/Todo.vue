<template>
    <div class="tile flex-centered">
              <div class="tile-icon">
                <i class="icon" :class="todo.checked ? 'icon-check' : 'icon-time'"></i>
              </div>
            <div class="tile-content">
              <div class="tile-subtitle">{{ todo.description }}</div>
            </div>
            <div class="tile-action">
              <button @click="$emit('toggle', todo)" class="btn btn-link">
                <span v-if="todo.checked">Desmarcar</span>
                <span v-else>Concluir</span>
              </button>
              <button class="btn btn-link" @click="$emit('remove', todo)">
                <span class="text-error">Remover</span>
              </button>
            </div>
          </div>
</template>

<script>
export default {
    props: {
        todo: { type: Object, required: true }
    }
}
</script>