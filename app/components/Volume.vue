<template>
    <Page class="page">
        <ActionBar class="ab">
            <NavigationButton android.systemIcon="ic_menu_back" @tap="GoToHome()" class="header" />
            <Label text="Объём" class="header"/>
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
                    {name: 'МиллиЛитров', coef: 1, forInput: 0},
                    {name: 'Литров', coef: 10**3, forInput: 0},
                    {name: 'СантиМетров куб.', coef: 1, forInput: 0},
                    {name: 'ДециМетров куб.', coef: 10**3, forInput: 0},
                    {name: 'Метров куб.', coef: 10**6, forInput: 0},
                    {name: 'КилоМетров куб.', coef: 10**15, forInput: 0},
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