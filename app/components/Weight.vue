<template>
    <Page>
        <ActionBar>
            <Label text="Weight"/>
        </ActionBar>

        <GridLayout rows="*" columns="*">
            <Button text="ToHome" @tap="GoToHome()" />
        </GridLayout>
    </Page>
</template>

<script>
import Home from './Home.vue';
    export default {
        data () {
            return {
            };
        },
        methods: {
            GoToHome: function() {
                this.$navigateTo(Home);
            }
        }
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>