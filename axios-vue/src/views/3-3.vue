<template>
  
</template>

<script>
// @ is an alias to /src

//拦截器： 在请求或响应被处理前拦截它们
import axios from 'axios'
export default {
  name: 'axios3-3',
  created(){
   //请求拦截器
   axios.interceptors.request.use(
       config => {
           //在发送请求前做些什么
           return config
       },err =>{
           //在请求错误时做些什么 
           return Promise.reject(err)
        //    Promise.resolve 成功时候用
        //    Promise.reject 失败时候用
       }
   )

    //响应拦截器
    axios.interceptors.response.use(
        res => {
            //请求成功对响应数据的处理
            return res 
        }, err => {
            //响应错误做些什么
            return Promise.reject(err)
    })

    axios.get().then(res => {}).catch(err => {})

    //取消拦截器
    let interceptors = axios.interceptors.request.use(
        config => {
            config.headers = {
                auth: true
            }
            return config
    })

    axios.interceptors.request.eject(interceptors)

    //例子  登录状态 （token:''）
    //需要登录的接口
    let instance = axios.create({})
    instance.interceptors.request.use(
        config => {
            config.headers.token = ''
            return config
    })
    //不需要登录的接口
    let newInstance = axios.create({})

    
    //移动端开发(接口请求时添加提示弹窗的)
    let instance_phone = axios.create({})

    instance_phone.interceptors.request.use(
        config => {
            $('#modal').show()
            return config
        }
    )
    instance_phone.interceptors.response.use(
        res => {
            $('#modal').hide()
            return res
        }
    )

  }
}
</script>
