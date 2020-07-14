<template>
    <div id="app">
        <a-row type="flex">
            <a-col :span="6">
                <SideBar :blob="blob"
                         @select-category="selectedCategory = $event"
                         @select-status="selectedStatus = $event"
                ></SideBar>
            </a-col>
            <a-col :span="18">
                <Map :blob="blob"
                     :selectedCategory="selectedCategory"
                     :selectedStatus="selectedStatus"
                ></Map>
            </a-col>
        </a-row>
    </div>
</template>

<script>
    import SideBar from './components/SideBar';
    import Map from './components/Map';
    import testBlob from './data/testBlob.json';

    export default {
        name: 'App',
        data() {
            return {
                blob: testBlob,
                selectedCategory: '',
                selectedStatus: ''
            }
        },
        components: {
            SideBar,
            Map
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        height: 100%;
        padding: 2em;
    }

    .mapboxgl-popup-content {
        padding: 1em;
    }

    .sidebar-filters > .a-menu {
        height: 100%;
    }

    #app > .ant-row-flex {
        height: 100%;
        overflow-y: hidden;
    }
</style>
