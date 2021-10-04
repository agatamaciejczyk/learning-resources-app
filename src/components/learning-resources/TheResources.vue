<template>
  <base-card>
    <base-button
      :mode="storedResButtonMode"
      @click="setSelectedTab('stored-resources')"
    >
      Stored Resources
    </base-button>
    <base-button
      :mode="addResButtonMode"
      @click="setSelectedTab('add-resource')"
    >
      Add Resource
    </base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab" />
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removerResource,
    };
  },
  data: () => ({
    selectedTab: 'stored-resources',
    storedResources: [
      {
        id: 'official-guide',
        title: 'Official Guide',
        description: 'The official Vue.js documentation',
        link: 'https://vuejs.org',
      },
      {
        id: 'google',
        title: 'Google',
        description: 'Learn to google...',
        link: 'https://google.come',
      },
    ],
  }),
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? '' : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? '' : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removerResource(resId) {
      const resIndex = this.storedResources.findIndex((res) => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>

<style>

</style>
