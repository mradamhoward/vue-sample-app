<template>
    <base-card>
        <the-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</the-button>
        <the-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resources</the-button>
    </base-card>
    <keep-alive>
    <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue'

export default {
    components: {
        StoredResources,
        AddResource
    },
    data(){
        return{
            selectedTab: 'stored-resources',
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js docs',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'The best search engine',
                    link: 'https://google.com'
                }
            ]
        };
    },
    computed: {
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat'
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resource' ? null : 'flat'
        }
    },
    provide(){
        return {
            resources: this.storedResources,
            addResources: this.addResources,
            deleteResource: this.removeResource
        };
    },
    methods: {
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addResources(title, desc, url){
            const newResource = {
                id: new Date().toISOString(), 
                title: title,
                description: desc,
                link: url
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';

        },
        removeResource(resId){
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        }
    }
}
</script>