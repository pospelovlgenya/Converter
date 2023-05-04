<template>
    <Page class="page">
        <ActionBar class="ab">
            <Label text="Converter" class="header"/>
        </ActionBar>

        <FlexboxLayout flexDirection="column" class="fl">
            <Button v-for="page in pages" :key="page.id" :row="page.id" :text="page.name" @tap="Go(page.id)" class="home-button" />
        </FlexboxLayout>
    </Page>
</template>

<script>
import Data from './Data.vue';
import Temperature from './Temperature.vue';
import Time from './Time.vue';
import Volume from './Volume.vue';
import Weight from './Weight.vue';

    export default {
        data () {
            return {
                pages: [
                    {id: 0, name: 'Данные', value: Data},
                    {id: 1, name: 'Температура', value: Temperature},
                    {id: 2, name: 'Время', value: Time},
                    {id: 3, name: 'Объём', value: Volume},
                    {id: 4, name: 'Вес', value: Weight},
                ]
            };
        },
        methods: {
            Go: function(id) {
                this.$navigateTo(this.pages[id].value);
            }
        }
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>
