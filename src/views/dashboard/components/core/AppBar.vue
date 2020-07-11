<template>
  <v-app-bar
    absolute
    app
    color="transparent"
    flat
    height="75"
    style="width: auto;"
  >
    <!-- <v-btn
      fab
      small
      @click="$vuetify.breakpoint.smAndDown ? setDrawer(!drawer) : $emit('input', !value)"
    >
      <v-icon v-if="value">
        mdi-view-quilt
      </v-icon>

      <v-icon v-else>
        mdi-dots-vertical
      </v-icon>
    </v-btn> -->

    <!-- <v-toolbar-title
      class="hidden-sm-and-down"
      v-text="$route.name"
    /> -->

    <!-- <v-spacer /> -->

    <v-toolbar-title
      class="hidden-sm-and-down"
    >
      {{ "TicketApp" }}
    </v-toolbar-title>

    <v-spacer />

    <!-- <v-text-field
      :label="$t('search')"
      color="secondary"
      hide-details
      class="mb-2"
      style="max-width: 165px;"
    >
      <template
        v-if="$vuetify.breakpoint.mdAndUp"
        v-slot:append-outer
      >
        <v-btn
          class="mt-n2"
          fab
          small
        >
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
      </template>
    </v-text-field> -->

    <div class="mx-3" />

    <!-- <v-btn
      min-width="0"
      text
    >
      <v-icon>mdi-view-dashboard</v-icon>
    </v-btn> -->

    <!-- <v-menu
      bottom
      left
      offset-y
      origin="top right"
      transition="scale-transition"
    >
      <template v-slot:activator="{ attrs, on }">
        <v-btn
          min-width="0"
          text
          v-bind="attrs"
          v-on="on"
        >
          <v-badge
            color="red"
            overlap
          >
            <template v-slot:badge>
              <span class="caption">5</span>
            </template>

            <v-icon>mdi-bell</v-icon>
          </v-badge>
        </v-btn>
      </template>

      <v-list
        :tile="false"
        nav
      >
        <div>
          <app-bar-item
            v-for="(n, i) in notifications"
            :key="`item-${i}`"
          >
            <v-list-item-title v-text="n" />
          </app-bar-item>
        </div>
      </v-list>
    </v-menu> -->

    <!-- <v-menu
      bottom
      left
      min-width="200"
      offset-y
      origin="top right"
      transition="scale-transition"
    >
      <template v-slot:activator="{ attrs, on }">
        <v-btn
          min-width="0"
          text
          v-bind="attrs"
          v-on="on"
        >
          <v-icon>mdi-account</v-icon>
        </v-btn>
      </template>

      <v-list
        :tile="false"
        flat
        nav
      >
        <template v-for="(p, i) in profile">
          <v-divider
            v-if="p.divider"
            :key="`divider-${i}`"
            class="mb-2 mt-2"
          />

          <app-bar-item
            v-else
            :key="`item-${i}`"
            to="/"
          >
            <v-list-item-title v-text="p.title" />
          </app-bar-item>
        </template>
      </v-list>
    </v-menu> -->
  </v-app-bar>
</template>

<script>
  // Components
  // import { VHover, VListItem } from 'vuetify/lib'

  // Utilities
  import { mapState, mapMutations } from 'vuex'

  export default {
    name: 'DashboardCoreAppBar',

    components: {
      // AppBarItem: {
      //   render (h) {
      //     return h(VHover, {
      //       scopedSlots: {
      //         default: ({ hover }) => {
      //           return h(VListItem, {
      //             attrs: this.$attrs,
      //             class: {
      //               'black--text': !hover,
      //               'white--text secondary elevation-12': hover,
      //             },
      //             props: {
      //               activeClass: '',
      //               dark: hover,
      //               link: true,
      //               ...this.$attrs,
      //             },
      //           }, this.$slots.default)
      //         },
      //       },
      //     })
      //   },
      // },
    },

    props: {
      value: {
        type: Boolean,
        default: false,
      },
    },

    data: () => ({
      notifications: [
        'Mike John Responded to your email',
        'You have 5 new tasks',
        'You\'re now friends with Andrew',
        'Another Notification',
        'Another one',
      ],
      profile: [
        { title: 'Profile' },
        { title: 'Settings' },
        { divider: true },
        { title: 'Log out' },
      ],
      // entry: [
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': 1,
      //         'd:RowKey': 1,
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:16:52.6128069Z',
      //         },
      //         'd:Candidato': 'Hugo Chavez',
      //         'd:Posicion': 'Java Dev',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'Angelica P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '20000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Pedro Paramo',
      //         'd:Posicion': 'Front Vue',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'Silvia P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '10000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Luis Perez',
      //         'd:Posicion': 'Front React',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'Keyvin D',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '15000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Pedro Paramo',
      //         'd:Posicion': 'Front Java',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'Keyvin D',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '16000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Angel Paez',
      //         'd:Posicion': 'Front Angular',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'Silvia P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '12000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Angel Paez',
      //         'd:Posicion': 'Front Vue',
      //         'd:Seniority': 'QA',
      //         'd:Reclutador': 'Angelica P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '10000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Erick Perez',
      //         'd:Posicion': 'Front CSS',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'Angelica P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '9000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Erick Perez',
      //         'd:Posicion': 'Front Vue',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'Keyvin D',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '20000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Angel Paez',
      //         'd:Posicion': 'Front Java',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'Angelica P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '17000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Jose Baes',
      //         'd:Posicion': 'Front Angular',
      //         'd:Seniority': 'QA',
      //         'd:Reclutador': 'Keyvin D',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '10000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Jose Baes',
      //         'd:Posicion': 'Front React Native',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'Silvia P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '10000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Erick Perez',
      //         'd:Posicion': 'Front Flutter',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'Angelica P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '12500',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Ana Riera',
      //         'd:Posicion': 'Front React Native',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'Keyvin D',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '10000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Hugo Chavez',
      //         'd:Posicion': 'Front Flutter',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'David A',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '10000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Rafa Morles',
      //         'd:Posicion': 'Front React Native',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'David A',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '10500',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Jorge Lopez',
      //         'd:Posicion': 'Front Angular',
      //         'd:Seniority': 'Sr',
      //         'd:Reclutador': 'Angelica P',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '16000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Jorge Lopez',
      //         'd:Posicion': 'Front Java',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'David A',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '11000',
      //         },
      //       },
      //     },
      //   },
      //   {
      //     content: {
      //       '-type': 'application/xml',
      //       'm:properties': {
      //         'd:PartitionKey': '1',
      //         'd:RowKey': '2',
      //         'd:Timestamp': {
      //           '-m:type': 'Edm.DateTime',
      //           '#text': '2020-04-02T21:17:47.652516Z',
      //         },
      //         'd:Candidato': 'Rafa Morles',
      //         'd:Posicion': 'Front Vue',
      //         'd:Seniority': 'Jr',
      //         'd:Reclutador': 'Keyvin D',
      //         'd:Salario': {
      //           '-m:type': 'Edm.Int32',
      //           '#text': '11500',
      //         },
      //       },
      //     },
      //   },
      // ],
    }),

    computed: {
      ...mapState(['drawer']),
    },

    methods: {
      ...mapMutations({
        setDrawer: 'SET_DRAWER',
      }),
    },
  }
</script>
