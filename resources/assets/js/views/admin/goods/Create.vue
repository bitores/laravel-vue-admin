<template>
    <div class="row">
        <div class="col-xs-12">

            <div class="box box-primary">
                <div class="box-header with-border">
                    <h3 class="box-title">{{$route.name}}</h3>
                </div>
                <div class="box-body">
                    <div class="form-group">
                        <label>商品名称</label>
                        <input type="text" class="form-control" v-model="goods.name"
                               placeholder="输入商品名称">
                    </div>
                    <div class="form-group">
                        <label>价格</label>
                        <input type="text" class="form-control" v-model="goods.price" placeholder="输入价格">
                    </div>

                    <image-upload label="上传产品图片" v-on:pic="getPicture"></image-upload>

                    <div class="form-group">
                        <label>关键词(淘宝搜索用)</label>
                        <input type="text" class="form-control" v-model="goods.tag"  placeholder="输入关键词">
                    </div>




                </div>
                <div class="box-footer">
                    <button type="submit" class="btn btn-default" @click="$router.back();">返回</button>
                    <button type="submit" class="btn btn-info pull-right" @click="add">添加</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import vSelect from 'vue-select';
    import ImageUpload  from '../../../components/admin/ImageUpload.vue';
    export default{
        components: {vSelect, 'image-upload': ImageUpload},
        data () {
            return {
                goods: {
                    name: '',
                    price: '',
                    tag: '',
                    picture: '',
                }

            }
        },

        created () {


        },
        methods: {
            add(){
                var url = '/admin/goods';

                this.callHttp("POST", url, this.goods, function (json) {
                    if (json.status) {
                        toastr.success('添加商品成功!')
                        this.$router.back();
                    }
                });

            },
            getPicture(value){
                this.goods.picture = value;
            }
        }
    }
</script>