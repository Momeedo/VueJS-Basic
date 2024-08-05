<template>
    <div class="basic">
        <h1>This is a demo page of basic VueJS features</h1>
    </div>
    <div class="spacing"></div>
    <PropsDemo :propFromParent="propFromBasicPage"></PropsDemo>
    <div class="spacing"></div> 
    <div>
        <div v-if="!keywords.length">No Keywords in the list.</div>
        <div v-text="'There are ' + keywords.length + ' element(s)'"></div>
        <div>There are {{ keywords.length }} element(s)</div>
        <div class="spacing"></div>
        <div class="keywords-input-wrapper">
            <span v-for="(keyword, index) in keywords" :key="index" class="keyword-item">
                {{ index + " : " + keyword }} <a class="remove-keyword" href="#"
                    v-on:click.prevent="deleteKeyword(index)">x</a>
            </span>
            <input type="text" class="keyword-input" v-model.trim="newKeyword"
                placeholder="Type Keyword (Enter or Tab to validate)" :class="{ 'keyword-exists': keywordExists }"
                v-on:keydown.enter="keywords.push($event.target.value)"
                v-on:keydown.tab.prevent="keywords.push($event.target.value)" v-on:keydown.delete="deleteLastKeyword" />
        </div>
        <div>
            <button v-on:click="addKeyword">Add {{ newKeyword }}</button>
        </div>
    </div>
</template>

<script>
import PropsDemo from '../components/PropsDemo.vue'
export default {
    watch: {
        newKeyword(newKey, oldKey) {
            console.log("Input Keyword changed from " + oldKey + " to " + newKey + ".");
            if (newKey.indexOf(",") > -1) {
                this.newKeyword = this.newKeyword.slice(0, -1);
                this.addKeyword();
            }
        }
    },
    computed: {
        keywordExists() {
            return this.keywords.includes(this.newKeyword);
        }
    },
    methods: {
        addKeyword() {
            this.newKeyword && !this.keywordExists ? this.keywords.push(this.newKeyword) : null;
            this.newKeyword = "";
        },
        deleteKeyword(index) {
            this.keywords.splice(index, 1);
        },
        deleteLastKeyword() {
            if (this.newKeyword.length === 0) {
                this.deleteKeyword(this.keywords.length - 1);
            }
        }
    },
    data() {
        return {
            keywords: ["Sports", "Cinema", "Music"],
            newKeyword: "",
            propFromBasicPage: ["VueJS", "Laravel", "DevOps"],
        }
    },
    components: {
        PropsDemo
    },
    mounted() {
        setTimeout(() => {
            this.propFromBasicPage.push("ReactJS");
        }, 3000)
    }

}
</script>

<style>
@media (min-width: 1024px) {
    .basic {
        min-height: 100vh;
        display: flex;
        align-items: center;
    }
}

.basic h1 {
    margin-top: 30px;
    text-align: center;
}

hr {
    margin: 5vh;
}

input {
    width: 100%;
}

.spacing {
    margin-top: 10px;
}

.keyword-exists {
    color: red;
}

button {
    color: white;
    background-color: hsla(160, 100%, 37%, 1);
    padding: 8px;
    padding-right: 15px;
    padding-left: 15px;
}

.keywords-input-wrapper {

    padding: 0.5em;
    border: 1px solid #dbdbdb;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    min-height: 36px;
    box-sizing: border-box;
}

.keyword-item {
    color: #212529;
    background-color: #eee;
    margin-right: 0.3em;
    padding: 0.25em 0.4em;
    font-size: 75%;
    line-height: 1;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding-right: 1.25em;
    padding-left: 0.6em;
}

.tag-keyword {
    color: #495057;
    flex: 1;
    background: transparent;
    border: none;
}

.keyword-input:focus {
    outline: none;
}

a.remove-keyword {
    text-decoration: none;
}
</style>