<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://cdn.vuetifyjs.com/images/john.png"></v-img>
          </v-list-item-avatar>
        </v-list-item>

        <v-list-item link>
          <v-list-item-content>
            <v-list-item-title class="title">
              {{ user.username }}
            </v-list-item-title>
            <v-list-item-subtitle>{{ user.email }}</v-list-item-subtitle>
          </v-list-item-content>

          <v-list-item-action>
            <v-icon>mdi-menu-down</v-icon>
          </v-list-item-action>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-list>
        <v-list-group
          v-for="(group, index) in groups"
          :value="false"
          :key="index"
          no-action
        >
          <v-icon
            slot="prependIcon"
            v-html="group.icon"
          ></v-icon>
          <template v-slot:activator>
            <v-list-item-title>{{ group.title }}</v-list-item-title>
          </template>
          <v-list-item
            v-for="({title, icon, to}, i) in group.items"
            :key="i"
            :to="to"
            router
          >
            <v-list-item-title v-text="title"></v-list-item-title>
            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
          </v-list-item>
        </v-list-group>
      </v-list>
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"/>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"/>
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="clipped = !clipped"
      >
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="fixed = !fixed"
      >
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title"/>
      <v-spacer/>
      <v-btn
        icon
        @click.stop="rightDrawer = !rightDrawer"
      >
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt/>
      </v-container>
    </v-main>
    <v-navigation-drawer
      v-model="rightDrawer"
      :right="right"
      temporary
      fixed
    >
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>

export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        },
        {
          icon: 'mdi-currency-usd-circle',
          title: 'Finance',
          to: '/finance'
        },
        {
          icon: 'mdi-adjust',
          title: 'Stations',
          to: '/stations'
        },
        {
          icon: 'mdi-calendar-month',
          title: 'Calendar',
          to: '/calendar'
        },
        {
          icon: 'mdi-clipboard-file',
          title: 'Reports',
          to: '/reports'
        },
        {
          icon: 'mdi-cog-outline',
          title: 'Settings',
          to: '/settings'
        }
      ],
      groups: [
        {
          title: 'Patients',
          icon: 'mdi-account-multiple',
          items: [
            {
              icon: 'mdi-alarm-multiple',
              title: 'Appointments',
              to: '/appointments'
            },
            {
              icon: 'mdi-account-multiple',
              title: 'Patients',
              to: '/patients'
            },
            {
              icon: 'mdi-alpha-o-circle',
              title: 'OPD',
              to: '/opd'
            },
            {
              icon: 'mdi-bed-queen',
              title: 'IPD',
              to: '/ipd'
            }
          ],
        },
        {
          title: 'Inventory',
          icon: 'mdi-store-24-hour',
          items: [
            {
              icon: 'mdi-pharmacy',
              title: 'Inventory',
              to: '/inventory'
            },
            {
              icon: 'mdi-pill',
              title: 'Medicine',
              to: '/medicine'
            },
            {
              icon: 'mdi-home-floor-1',
              title: 'Wards',
              to: '/ward'
            },
            {
              icon: 'mdi-bunk-bed-outline',
              title: 'Beds',
              to: '/bed'
            }
          ],
        },
        {
          title: 'Laboratory',
          icon: 'mdi-store-24-hour',
          items: [
            {
              icon: 'mdi-octagon',
              title: 'Laboratory',
              to: '/laboratory'
            },
            {
              icon: 'mdi-radioactive',
              title: 'Radiology',
              to: '/radiology'
            }
          ],
        },
        {
          title: 'Organization',
          icon: 'mdi-store-24-hour',
          items: [
            {
              icon: 'mdi-account-hard-hat',
              title: 'Staffs',
              to: '/staffs'
            },
            {
              icon: 'mdi-office-building',
              title: 'Departments',
              to: '/departments'
            },
            {
              icon: 'mdi-help-circle',
              title: 'Service',
              to: '/service'
            }
          ],
        }
      ],

      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },

  computed: {
    user() {
      return this.$store.state.auth.user
    }
  }
}
</script>
