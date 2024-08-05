<template>
    <div class="basic">
        <h1>This is a demo page of basic VueJS features</h1>
    </div>
    <div class="spacing"></div>
    <div>
        <div v-if="!keywords.length">No Keywords in the list.</div>
        <div v-text="'There are ' + keywords.length + ' element(s)'"></div>
        <div>There are {{ keywords.length }} element(s)</div>
        <div class="spacing"></div>
        <div v-for="(keyword, index) in keywords" :key="index">
            <ul>
                <li>{{ index + " : " + keyword }} <a href="#" v-on:click.prevent="deleteKeyword(index)">x</a></li>
            </ul>
        </div>
        <div class="spacing"></div>
        <div>
            <input type="text" v-model.trim="newKeyword" placeholder="Type Keyword (Enter or Tab to validate)"
                :class="{ 'keyword-exists': keywordExists }"
                v-on:keydown.enter="keywords.push($event.target.value)"
                v-on:keydown.tab.prevent="keywords.push($event.target.value)" v-on:keydown.delete="deleteLastKeyword" />
        </div>
        <div>
            <button v-on:click="addKeyword">Add {{ newKeyword }}</button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
    },
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
        }
    },

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
</style>