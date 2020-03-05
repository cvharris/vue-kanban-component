<template>
  <div>
    <h1>Board</h1>
    <div class="groups-container">
      <lane-group v-for="group in kanbanState" :key="group.id" :group="group">
        <lane v-for="lane in group.lanes" :key="lane.id" :lane="lane">
          <card v-for="card in lane.cards" :key="card.id" :card="card">
            <slot name="card" :card="card" />
          </card>
        </lane>
      </lane-group>
    </div>
  </div>
</template>

<script>
import LaneGroup from '~/components/LaneGroup'
import Lane from '~/components/Lane'
import Card from '~/components/Card'

export default {
  components: {
    LaneGroup,
    Lane,
    Card
  },
  props: {
    groups: {
      type: Array,
      required: true
    },
    lanes: {
      type: Array,
      required: true
    },
    cards: {
      type: Array,
      required: true
    }
  },
  computed: {
    groupState() {
      return this.normalizeState(this.groups)
    },
    laneState() {
      return this.normalizeState(this.lanes)
    },
    cardState() {
      return this.normalizeState(this.cards)
    },
    kanbanState() {
      return this.groupState.allIds.map((groupId) => {
        const group = this.groupState.byId[groupId]
        return {
          ...group,
          lanes: group.laneIds.map((laneId) => {
            const lane = this.laneState.byId[laneId]
            return {
              ...lane,
              cards: lane.cardIds.map((cardId) => this.cardState.byId[cardId])
            }
          })
        }
      })
    }
  },
  methods: {
    normalizeState(collection) {
      return collection.reduce(
        (state, item) => {
          state.allIds.push(item.id)
          state.byId[item.id] = item
          return state
        },
        { allIds: [], byId: {} }
      )
    }
  }
}
</script>

<style>
.groups-container {
  display: flex;
}
</style>
