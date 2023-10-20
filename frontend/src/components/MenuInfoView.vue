<template>

    <v-data-table
        :headers="headers"
        :items="menuInfo"
        :items-per-page="5"
        class="elevation-1"
    ></v-data-table>

</template>

<script>
    const axios = require('axios').default;

    export default {
        name: 'MenuInfoView',
        props: {
            value: Object,
            editMode: Boolean,
            isNew: Boolean
        },
        data: () => ({
            headers: [
                { text: "id", value: "id" },
            ],
            menuInfo : [],
        }),
          async created() {
            var temp = await axios.get(axios.fixUrl('/menuInfos'))

            temp.data._embedded.menuInfos.map(obj => obj.id=obj._links.self.href.split("/")[obj._links.self.href.split("/").length - 1])

            this.menuInfo = temp.data._embedded.menuInfos;
        },
        methods: {
        }
    }
</script>

