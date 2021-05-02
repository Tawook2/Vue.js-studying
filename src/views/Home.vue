<template>
    <div>
        <h1>Welcome to {{title2}}!</h1>
        <input type="text" v-model="input1"/>
        <button type="button" @click="getData">Get</button>
        <button type="button" @click="setData">Set</button>

        <!-- '{{}}' HTML 코드에 접근할때, ':' Attribute, 데이터 변수에 접근할떄-->
        <select class="form-control" v-model="region" @change="changeRegion">
            <option :key="i" :value="d.v" v-for="(d,i) in options">{{d.t}}</option>
        </select>

        <!-- v-if 조건 실패시 렌더링 조차 하지않는다 (사용자가 이용할지 애매하면 resource를 줄이기 위해 일단 v-if로 해놓는다)-->
        <!-- v-show 렌더링은 하는데 화면에 보여지지 않음(resource 절감을 위해 화면에 자주 보였다 사라졌다하면 이걸 쓴다) ex: 카테고리 -->
        <table class="table table-bordered" v-if="tableShow">
            <tr :key="i" v-for="(d,i) in options">
                <td>{{d.v}}</td>
                <td>{{d.t}}</td>
            </tr>
        </table>
    </div>
</template>
<script>
export default{
    data(){
        return{
            title: "개발자의 품격",
            title2: "Seoul",
            input1: "abcd",
            options : [
                {v:"S", t:"Seoul"},
                {v:"J", t:"Jeju"},
                {v:"B", t:"Busan"},
            ],
            region: "B",
            tableShow: true
        };
    },
    watch: {
        // 특정 데이터 항상 모니터링 할때 사용 (데이터가 바뀌는 순간 캐치를 해서 작업을 할떄)
        input1() {
            console.log(this.input1);
        },
        title(){},
    },
    methods: {
        getData(){
            alert(this.input1);
        },
        setData(){
            this.input1 = "12345";
        },
        changeRegion(){
            alert(this.region);
        }
    },
    // life cycle from vue.js document
    beforeCreate(){
        // 페이지가 component 값을 가져와서 로딩이 되기 전
        console.log("beforeCreate")
    },
    created(){
        // 페이지가 라우팅하기전에 미리 DB에서 값을 가져와 data()에 값을 바인딩 하는곳 (화면이 열리는 순간 데이터를 렌더링을 하고 싶을때)
        console.log("created")
    },
    beforeMount(){
        // 페이지가 component 값을 가져와서 로딩이 되는 곳
        console.log("beforeMount")
    },
    mounted(){
        // 바인딩 된 data 값을 보여줄 수 있다.
        console.log("mounted")
    },
    beforeUpdate(){
        // 데이터 변경 전 이벤트를 넣는 곳
        console.log("beforeUpdate")
    },
    updated(){
        // 데이터 변경 후 이벤트를 넣는 곳
        console.log("updated")
    },
    beforeDestroy(){
        console.log("beforeDestroy")
    },
    destroyed(){
        console.log("destroyed")
    }
};
</script>

