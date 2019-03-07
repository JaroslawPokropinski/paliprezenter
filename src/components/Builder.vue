<template>
    <div id="builder">
        <input type="text" v-model="text" class="builder-input">
        <div>
            <input type="button" value="Add Male" v-on:click="onAddMale()" class="builder-button">
            <input type="button" value="Add Female" v-on:click="onAddFemale()" class="builder-button">
            <input type="button" value="Add Pause" v-on:click="onAddPause()" class="builder-button">
            <input type="button" value="Play" v-on:click="onPlay([...list])" class="builder-button">
        </div>
        <ul class="builder-list">
            <li v-for="(m, index) in list" :key="m.id" class="builder-item"> {{ (m.pause) ? `Pause: ${m.timeout}ms` : `${m.voice}: ${m.text}` }} 
                <span class="cancel-button" v-on:click="onDelete(index)">
                    <img src="cancel.svg" width="16px" height="16px">
                </span>
            </li>
        </ul>
        
    </div>
</template>

<script>
export default {
    name: 'builder',
    data () {
        return {
            count: 0,
            text: '',
            list: []
        }
    },
    methods: {
        onAddMale () {
            if (this.text.length <= 0) {
                return
            }
            this.list.push({id: this.count, text: this.text, voice: 'male'})
            this.count ++
            this.text = ''
        },
        onAddFemale () {
            if (this.text.length <= 0) {
                return
            }
            this.list.push({id: this.count, text: this.text, voice: 'female'})
            this.count ++
            this.text = ''
        },
        onAddPause () {
            const timeout = parseInt(this.text)
            if (timeout) {
                this.list.push({id: this.count, pause: true, timeout})
                this.count ++
            }
            this.text = ''
        },
        onPlay (list) {
            if (list.length <= 0) {
                return
            }
            if (this.list[0].pause) {
                const l = list.shift()
                setTimeout(() => this.onPlay(), l.timeout)
                return
            }
            const voice = (list[0].voice === 'male') ? 'Polish Male' : 'Polish Female'
            responsiveVoice.speak(list.shift().text, voice, {onend: () => {
                this.onPlay(list)
            }})
        },
        onDelete (index) {
            this.list.splice(index, 1)
        }
    }
}
</script>

<style scoped>
#builder {
    display: flex;
    flex-direction: column;
}
.builder-input {
    font-family: 'Roboto', sans-serif;
    display: block;
    width: 100%;
    box-sizing:border-box;
    margin: 8px 0px;
    padding: 1rem 1rem;
    font-size: 2rem;
    border: 0;
    border-radius: 3px;
    background: #334a66;
}

.builder-button {
    font-family: 'Roboto', sans-serif;
    background-color: #c51f5d;
    border: none;
    color: white;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
    color: white;
}

.builder-list {
    text-align: left;
    list-style-type: none;
    margin: 0;
    padding: 0;
    
    overflow:hidden;
    overflow-y:auto;
}

.builder-item {
    display: block;
    color: white;
    padding: 14px 16px;
    margin-top: 4px;
    text-decoration: none;
    background-color: #334a66;
}
.cancel-button {
    float: right;
}

::-webkit-scrollbar {
    display: none;
}
</style>
