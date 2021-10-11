~~~~ js
import Vue from 'vue'
import Vuex from 'vuex'
import ls from '../assets/js/LStorage'
Vue.use(Vuex)
export default new Vuex.Store({
    state: {
        userInfo: {},
        diagType: 3,
        faceId: null, //上传的脸部id
        tongueId: null, //上传的舌头id
        answer: null, //问诊答案
        faceFile: null, //面诊图片
        tongueFile: null, //舌诊图片
        testUser: {}, //当前测试者的信息
        feedquestion: {}, //帮助问题获取
    },
    mutations: {
        //修改用户信息
        setUserInfo(state, info) {
            state.userInfo = info;
            ls.setItem('userInfo', info);
        },
        //修改评估流程（两诊还是三诊）
        setDiagnosis(state, type) {
            state.diagType = type;
            ls.setItem('diagType', type);
        },
        //修改脸部id
        setFaceId(state, id) {
            state.faceId = id;
            ls.setItem('faceId', id);
        },
        //修改舌头id
        setTongueId(state, id) {
            state.tongueId = id;
            ls.setItem('tongueId', id);
        },
        //修改问诊答案
        setAnswer(state, answer) {
            state.answer = answer;
            ls.setItem('answer', answer);
        },
        //修改面诊图片
        setFaceFile(state, file) {
            state.faceFile = file;
        },
        //修改舌诊图片
        setTongueFile(state, file) {
            state.tongueFile = file;
        },
        //修改当前测试者的信息
        setTestUser(state, info) {
            state.testUser = info;
            ls.setItem('testUser', info);
        },
        //获取帮助问题
        setFeed(state, info) {
            state.feedquestion = info;
            ls.setItem('feedquestion', info);
        },
    }
})
~~~~
~~~~js
this.$store.commit("setDiagnosis", 2);
~~~~