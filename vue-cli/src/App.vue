<template>
    <div>
        <myheader></myheader>
        <p v-if="msg.length > 0">
            {{msg}}
        </p>
        <p v-else>
            no text
        </p>
        <input type="text" v-model="msg">
        <button @click="clear()">clear</button>
        <button @click="change()">change</button>
    </div>
</template>

<script>
import myheader from './components/myheader'

export default {
    components: {
        myheader
    },
    data() {
        return {
            msg: 'Hello World!'
        }
    },
    methods: {
        clear() {
            this.msg = ''
        },
        change() {
          fetch('http://www.geonames.org/postalCodeLookupJSON?postalcode=20504&country=US')
            .then(response => {
                return response.json()
            })
            .then(json => {
                this.msg = json.postalcodes[0].adminName1
            })
            .catch((err) => {
                this.msg = err // エラー処理
            });
        }
    },
    created() {
        fetch('http://www.geonames.org/postalCodeLookupJSON?postalcode=10504&country=US')
            .then(response => {
                return response.json()
            })
            .then(json => {
                this.msg = json.postalcodes[0].adminName1
            })
            .catch((err) => {
                this.msg = err // エラー処理
            });
    }
}
</script>
