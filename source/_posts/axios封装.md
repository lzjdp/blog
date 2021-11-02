---
title: axios封装
date: 2021-10-29 14:22:22
tags:
---

```
import Axios from 'axios'

const request = Axios.create({
    baseUrl: '',
    timeout: 15000
})

request.inteceptor.request.use(config => {
    const token = window.localStorage.getItem('token')
    if (token) {
        config.headers['token'] = token
    }
    return config
})

request.inteceptor.response.use(response => {
    const res = response.data
    if (res.code !== 2000) {
        
    }
})

export default request
```