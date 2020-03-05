<template>
  <div class="container">
    <div>
      <h1 class="title">
        vue-kanban-lanes
      </h1>
      <h2 class="subtitle">
        Kanban lanes and card manager
      </h2>
      <div>
        <kanban-board :groups="groups" :lanes="lanes" :cards="cards">
          <template v-slot:card="{ card }">
            <h4>hi, {{ card.title }}</h4>
          </template>
        </kanban-board>
      </div>
    </div>
  </div>
</template>

<script>
import KanbanBoard from '~/components/KanbanBoard'

export default {
  components: {
    KanbanBoard
  },
  data() {
    return {
      groups: [
        {
          id: 'todo',
          title: 'TODO',
          laneIds: ['ideas', 'shaping', 'betting']
        },
        {
          id: 'doing',
          title: 'Doing',
          laneIds: ['design', 'dev', 'test', 'release']
        },
        {
          id: 'done',
          title: 'Done',
          laneIds: ['completed', 'trash']
        }
      ],
      lanes: [
        {
          id: 'ideas',
          title: 'Ideas',
          cardIds: []
        },
        {
          id: 'shaping',
          title: 'Shaping',
          cardIds: []
        },
        {
          id: 'betting',
          title: 'Betting',
          cardIds: ['wake']
        },
        {
          id: 'design',
          title: 'Design',
          cardIds: []
        },
        {
          id: 'dev',
          title: 'Dev',
          cardIds: []
        },
        {
          id: 'test',
          title: 'Test',
          cardIds: []
        },
        {
          id: 'release',
          title: 'Release',
          cardIds: []
        },
        {
          id: 'completed',
          title: 'Completed',
          cardIds: []
        },
        {
          id: 'trash',
          title: 'Trash',
          cardIds: []
        }
      ],
      cards: [
        {
          id: 'wake',
          title: 'Wake the damn kids'
        }
      ]
    }
  },
  methods: {
    getLaneById(laneId) {
      return this.lanes.find((lane) => lane.id === laneId)
    },
    getCardById(cardId) {
      return this.cards.find((card) => card.id === cardId)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
