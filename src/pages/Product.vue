<template>
    <div class="product">
        <van-list
        v-model="loading"
        :finished="finished"
        finished-text="没有更多了"
        @load="onLoad"
        >
            <van-card
            v-for="p in product"
            :key="p.id"
            :price="p.price"
            :desc="p.description"  
            :title="p.name"
            :thumb="p.photo"
            >
            <div slot="footer">
                <van-stepper min="0" v-model="p.index" @change="numChangeHandler(p.price,$event)"/>
            </div>
            </van-card>
        </van-list>
        <van-submit-bar
        :price="3050"
        button-text="Submit"
        @submit="onSubmit"
        />
    </div>
</template>
<script>
import {mapActions,mapMutations,mapState} from 'Vuex'
export default {
    data(){
        return{
            value:0,
              loading: false,
              finished: false,
            categoryId:this.$route.query.categoryId,
        }
    },
    created(){
        this.findAllProducts()
        this.findByCategoryId(this.categoryId)
        this.onLoad()
    },
    computed:{
        ...mapState('product',['products','product'])
    },
    methods:{
        ...mapActions('product',['findAllProducts','findByCategoryId']),
        numChangeHandler(val,event){
            console.log(val,event)
        },
        onLoad() {
            // 异步更新数据
            setTimeout(() => {
                // 加载状态结束
                this.loading = false;
                // 数据全部加载完成
                if (this.product.length) {
                this.finished = true;
                }
            }, 100);
        },
    }
}
</script>