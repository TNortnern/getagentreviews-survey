<template>
  <v-container id="logout">
    <v-overlay :value="bulk">
      <v-progress-circular indeterminate size="64" />
    </v-overlay>
    <v-snackbar
      v-model="failed"
      top
      :timeout="5000"
    >
      <template v-if="failed.length">
        <h2>Failed Items</h2>
        <span v-for="item in failed" :key="item.id">
          {{ item.client.id }}
        </span>
      </template>
    </v-snackbar>
    <v-row justify-xl="space-between" justify-lg="space-between" justify="center">
      <v-col :lg="cols.lg" :md="cols.md" :sm="cols.sm" :cols="cols.reg">
        <DashboardTopCard card-type="positive" />
      </v-col>
      <v-col :lg="cols.lg" :md="cols.md" :sm="cols.sm" :cols="cols.reg">
        <DashboardTopCard card-type="negative" />
      </v-col>
      <v-col :lg="cols.lg" :md="cols.md" :sm="cols.sm" :cols="cols.reg">
        <DashboardTopCard card-type="pending" />
      </v-col>
      <v-col :lg="cols.lg" md="3" cols="6">
        <span style="font-size: 14px;" class="text--grey font-weight-bold text-center ml-4">
          <v-icon x-small class="mr-2 text--grey bold">mdi-tab</v-icon>Notification
        </span>
        <v-btn
          class="d-block"
          rounded
          style="color: blue; border: 1px solid blue;"
        >
          Refer & Earn
        </v-btn>
        <v-btn
          dark
          color="red"
          class="d-block"
          rounded
        >
          Gmail Connected
        </v-btn>
        <v-btn
          dark
          color="#6b79ed"
          class="d-block"
          rounded
          @click.stop="$store.commit('dashboardTop/setModal', {modalType: 'addingPeople', to: true} )"
        >
          (+) Add People
        </v-btn>
      </v-col>
      <AddPeople />
    </v-row>
  </v-container>
</template>

<script>
import DashboardTopCard from '~/components/dashboard/DashboardTop/DashboardTopCard'
import AddPeople from '~/components/dashboard/DashboardTop/AddPeople'
export default {
  components: {
    DashboardTopCard,
    AddPeople
  },
  data () {
    return {
      cols: {
        reg: '10',
        sm: '6',
        md: '4',
        lg: '3'
      }
    }
  },
  computed: {
    bulk: {
      get () {
        return this.$store.state.clients.bulk.value
      },
      set (val) {
        this.$store.commit('clients/setBulk', { value: false })
      }
    },
    failed: {
      get () {
        return this.$store.state.clients.bulk.failed && this.$store.state.clients.bulk.failed.length
      },
      set () {
        this.$store.commit('clients/setBulk', { failed: [] })
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~/styles';
.dashboard-top {
  @include large('down') {
    flex-wrap: wrap !important;
    justify-content: center !important;
  }
}
.dashboard-top__buttons {
  @include large('down') {
    width: 350px;
    text-align: center;
    margin-top: 10px;
  }
}
button {
  margin: 5px 0;
  width: 144px;
  font-size: 12px !important;
}
</style>
