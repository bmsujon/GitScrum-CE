<script>
export default {
  data() {
    return {
      data: [
        {
          title: this.$t('Project'),
        },
        {
          label: this.$t('Details'),
          route: 'project.settings.details',
        },
        {
          label: this.$t('API Management'),
          route: 'project.settings.api-management',
        },
        {
          label: this.$t('Integrations'),
          route: 'projects.integrations',
        },
        {
          space: true,
        },
        {
          title: this.$t('Project Templates'),
        },
        {
          label: this.$t('Workflow'),
          route: 'project.settings.templates',
          template: 'workflow'
        },
        {
          label: this.$t('Task Type'),
          route: 'project.settings.templates',
          template: 'type'
        },
        {
          label: this.$t('Task Effort'),
          route: 'project.settings.templates',
          template: 'effort'
        },
        {
          label: this.$t('Task Custom Field'),
          route: 'project.settings.templates',
          template: 'field'
        },
        {
          label: this.$t('Task Checklist'),
          route: 'project.settings.templates',
          template: 'checklist'
        },
        {
          label: this.$t('User Story Priority'),
          route: 'project.settings.templates',
          template: 'priority'
        },
      ],
    }
  },
  methods:{
    getAtive(item){
      
      let current, params

      if ( item.route ){
        if (item.template){ 
          params = { name: item.route, params: { template: item.template } }
        } else {
          params = { name: item.route }
        }

        current = this.$router.resolve( params ).href

        if ( current === window.location.pathname){
          return true
        }
      }
      return false

    }
  }
}
</script>

<template>
  <nav v-not-visible="'tablet'" class="sidebar sidebar-offcanvas">
    <ul class="nav">
      <li class="nav-item">
        <ul class="nav submenu-wrapper">
          <li v-for="item in data" :key="item.route" class="nav-item" :class="{ ' nav-active ': getAtive(item) }">
            <div v-if="item.space" class="mt-2"> </div>
            <div v-if="item.title" class="sidebar-menu-title">{{ item.title }}</div>
            <router-link v-if="item.template === 'undefined'" :to="{ name: item.route }" class="nav-link">
              <span class="menu-title">{{ item.label }}</span>
            </router-link>
            <router-link else :to="{ name: item.route, params: { template: item.template } }" class="nav-link">
              <span class="menu-title">{{ item.label }}</span>
            </router-link>
          </li>
        </ul>
      </li>
    </ul>
  </nav>
</template>
