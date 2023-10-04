<script setup>
import { guardReactiveProps, onMounted, onUpdated, ref, watch } from 'vue';
import {
    app,
    auth,
    database,
    ref as refDb,
    set,
    push,
    onValue,
    remove,
    child,
    get

} from '../firebaseConfig'
import { async } from '@firebase/util';
import { object } from 'webidl-conversions';

let chat = ref("");
let histories = ref([]);
let historyKey = ref("");
const bottomEl = ref(null);
const studentId = "6314110010";
let refChat;
const db = refDb(database, 'all_chat/');

const onSend = () => {
    if (chat.value != '' && histories.value != '') {
        push(refDb(database, `all_chat/${historyKey.value}`), {
            "user": studentId,
            "message": chat.value,
            "dateTime": new Date().toISOString()
        });
        chat.value = "";
    }
}
onValue(db, (snapshot) => {
    histories.value = snapshot.val() ?? [];
})
onUpdated(() => {
    bottomEl.value.scrollIntoView({ behavior: 'smooth' });
})
const selectGroup = (key) => {
    historyKey.value = key;
}
let groupChatName = ref("");
const createGroup = () => {
    if (groupChatName.value != '') {
        get(child(db, `${groupChatName.value}`)).then((snapshot) => {
            if (snapshot.exists()) {
                alert("Cannot Create");
            } else {
                push(refDb(database, `all_chat/${groupChatName.value}`), {
                    "user": studentId,
                    "message": '',
                    "dataTime": new Date().toISOString()
                });
            }
            groupChatName.value = '';
        }).catch((err) => {
            console.error(err);
        })


    }
}
const deleteGroup = (data) => {
    remove(refDb(database, `all_chat/${data}`));
    window.location.reload();
}
</script>

<template>
    <div class="flex">
        <div class="bg-white h-[90vh] w-[30%]">
            <div class="overflow-y-scroll w-full h-[90%]">
                <div class="card card-slde bg-base-100 shadow-xl w-full mb-4" style="cursor: pointer;"
                    v-for="(group, index) in histories" :key="index" data-theme="valentine" @click="selectGroup(index)">
                    <div class="card-body">
                        <h2 class="card-title">{{ index }}</h2>

                        <div class="flex">
                            <p>{{ group[Object.keys(group)[Object.keys(group).length - 1]]?.message }}</p>
                            <button class="btn" @click="deleteGroup(index)">delete</button>
                        </div>
                        <!-- <p>{{ group[object.keys(group)[]] }}</p> -->
                    </div>
                </div>
            </div>
            <div class="w-full h-[10%] pt-4">
                <button class="btn w-full h-full" data-theme="valentine" onclick="my_modal_1.showModal()">Add Group</button>
                <dialog id="my_modal_1" class="modal">
                    <div class="modal-box">
                        <div class="form-control w-full">
                            <label class="label">
                                <span class="label-text">Group Name</span>
                            </label>
                            <input type="text" v-model="groupChatName" placeholder="Type here"
                                class="input input-bordered w-full" />
                        </div>

                        <div class="modal-action">
                            <form method="dialog">
                                <!-- if there is a button in form, it will close the modal -->
                                <button class="btn btn-success btn-outline" @click="createGroup()">Save</button>
                                <button class="btn btn-error btn-outline">Close</button>
                            </form>
                        </div>
                    </div>
                </dialog>
            </div>

        </div>
        <div class="bg-gray-50 h-[90vh] w-[70%]">
            <div class="overflow-y-scroll h-[90%] p-5 card">
                <div v-for="(history, index) in histories[historyKey]"
                    :class="`chat ${history.user == studentId ? 'chat-end' : 'chat-start'}`" :key="index">
                    <div class="chat-header">
                        {{ history.user }}
                        <time class="text-xs opacity-50"> {{ history.dateTime }}</time>
                    </div>
                    <div className="chat-bubble">{{ history.message }}</div>
                </div>
                <div ref="bottomEl"></div>
            </div>
            <div class="flex h-[10%]">
                <input v-on:keyup.enter="onSend" v-model="chat" type="text" placeholder="Enter Chat"
                    class="input input-bordered w-[80%] h-full">
                <button @click="onSend" class="w-[20%] btn h-full">Send</button>
            </div>
        </div>
    </div>
</template>
<style scoped></style>