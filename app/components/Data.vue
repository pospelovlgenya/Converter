<template>
    <Page class="page">
        <ActionBar class="ab">
            <NavigationButton android.systemIcon="ic_menu_back" @tap="GoToHome()" class="header" />
            <Label text="Данные" class="header"/>
        </ActionBar>

        <FlexboxLayout flexDirection="column">
            <FlexboxLayout flexDirection="column">
                <Label text="Величина для конвертации:" class="text"/>
                <TextField v-model="inputValue" keyboardType="number" class="text"/>
                <ListPicker :items="getValues()" v-model="selectedValue" class="text"/>
            </FlexboxLayout>
            <FlexboxLayout flexDirection="column">
                <Label text="Это равняется:" class="text"/>
                <Label v-for="value in values" :key="value.name" class="text">{{ value.forInput }} {{ value.name }}</Label>
            </FlexboxLayout>
        </FlexboxLayout>
    </Page>
</template>

<script>
import Home from './Home.vue';
    export default {
        data () {
            return {
                inputValue: 0,
                selectedValue: 0,
                values: [
                    {name: 'бит', coef: 2**0, forInput: 0},
                    {name: 'Байт', coef: 2**3, forInput: 0},
                    {name: 'КБ', coef: 2**13, forInput: 0},
                    {name: 'МБ', coef: 2**23, forInput: 0},
                    {name: 'ГБ', coef: 2**33, forInput: 0},
                    {name: 'ТБ', coef: 2**43, forInput: 0},
                    {name: 'ПБ', coef: 2**53, forInput: 0}
                ],
            };
        },
        watch: {
            inputValue: function() {
                this.getResult();
            },
            selectedValue: function() {
                this.getResult();
            },
        },
        methods: {
            GoToHome: function() {
                this.$navigateTo(Home);
            },
            getValues: function() {
                let comp = [];
                for (i = 0; i < this.values.length; i++) {
                    comp.push(this.values[i].name);
                }
                return comp;
            },
            getResult: function() {
                let input = this.inputValue * this.values[this.selectedValue].coef;
                input = input < 0 ? '-' : input;
                for (i = 0; i < this.values.length; i++) {
                    this.values[i].forInput = input / this.values[i].coef;
                }
            }
        },
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>