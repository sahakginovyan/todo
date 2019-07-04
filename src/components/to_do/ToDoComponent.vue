<template>
    <div class="main-content">
        <div class="heading">
            <h3>To-Do-list task</h3>
        </div>
        <div class="row-content">
            <div class="todo-list-content row-item">
                <div class="content">
                    <h2>To do:</h2>
                    <div class="row-content">
                        <div class="added-task">
                            <ul class="task-list">
                                <li v-for="(task,index) in tasks " class="task-item" v-bind:key="task.key">
                                    <p>{{task.title}}</p>
                                    <div class="buttons-group">
                                        <input class="styled-checkbox" :id="'styled-checkbox-' + index" type="checkbox"
                                               @change="done(task, index)">
                                        <label :for="'styled-checkbox-' + index"></label>
                                        <button class="action-btn delete" v-on:click="removeTask(task,index)">X</button>
                                    </div>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="add-task-content">
                        <div class="row-content row-todo">
                            <label for="taskName">Task</label>
                            <input type="text" id="taskName" class="task-name" v-model="newTask">
                        </div>
                        <div class="btn-content">
                            <button class="add-task-btn" type="button" v-on:click="addItem()">Save Item</button>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row-item">
                <table id="customers">
                    <tr>
                        <th>Title</th>
                    </tr>
                    <tr v-for="list  in doneLists" v-bind:key="list.key">
                        <td>{{list.list}}</td>
                    </tr>
                </table>
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                newTask: '',
                tasks: [],
                doneLists: [],
            };
        },
        methods: {
            addItem() {
                if (this.newTask) {
                    this.tasks.push({
                        title: this.newTask
                    });
                }
                this.newTask = '';
            },
            removeTask(task, index) {
                this.tasks.splice(index, 1);
            },
            done(task, index) {
                this.tasks.splice(index, 1);
                this.doneLists.push({
                    list: task.title,
                });
            },
        }
    }
</script>
<style scoped>
    .main-content {
        padding: 0 10%;
    }

    .heading h3 {
        font-weight: bold;
        margin-bottom: 50px;
    }

    .row-content {
        width: 100%;
        display: flex;
    }

    .row-todo {
        justify-content: flex-end;
    }

    .row-todo input {
        width: 85%;
        border-radius: 4px;
        border: 1px solid #e6e6e6;
        padding: 0 15px;
    }

    .row-todo input:focus {
        outline: none;
        box-shadow: none !important;
        border: unset !important;
    }

    .row-todo label {
        font-size: 20px;
        font-weight: bold;
        padding: 0 35px;
    }

    .btn-content {
        text-align: right;
    }

    .add-task-btn {
        height: 40px;
        padding: 0 15px;
        background: #3579b6;
        border: none;
        border-radius: 4px;
        color: #fff;
        margin-top: 20px;
    }

    .row-item {
        width: 50%;
        padding: 0 15px;

    }

    .content {
        width: 100%;
        min-height: 500px;
        height: auto;
        padding: 20px;
        background-color: #f5f5f5;
        border: 1px solid #e6e6e6;
        border-radius: 4px;
    }

    .todo-list-content .content h2 {
        font-size: 35px;
        text-align: left;
        font-weight: bold;
    }

    .added-task {
        width: 100%;
    }

    .task-list {
        width: 100%;
        padding: 0;
    }

    .task-item {
        list-style-type: none;
        height: 50px;
        max-height: 50px;
        background-color: #fff;
        border: 1px solid #e6e6e6;
        margin-bottom: 0;
        text-align: left;
        padding: 10px 15px;
        border-radius: 4px;
    }

    .task-item .buttons-group {
        float: right;
        display: flex;
    }

    .task-item p, .task-item div {
        display: inline-block;
    }

    .action-btn {
        width: 26px;
        height: 26px;
        border-radius: 2px;
        border: none;
        margin-left: 5px;
        color: #fff;
    }

    .action-btn.success {
        background-color: #5eb75e;
    }

    .action-btn.success img {
        display: block;
        width: 13px;
    }

    .action-btn.delete {
        background-color: #d5544d;
    }

    .styled-checkbox {
        position: absolute;
        opacity: 0;
    }

    .styled-checkbox + label {
        position: relative;
        cursor: pointer;
        padding: 0;
        width: 26px;
        height: 26px;
        border: 1px solid #5eb75e;
        border-radius: 2px;
    }

    .styled-checkbox + label:before {
        content: '';
        display: inline-block;
        width: 100%;
        height: 100%;
        background: white;
    }

    .styled-checkbox + label:before {
        background: #5eb75e;
    }

    .styled-checkbox + label:after {
        content: '';
        position: absolute;
        left: 7px;
        top: 10px;
        background: white;
        width: 2px;
        height: 2px;
        box-shadow: 2px 0 0 white,
        4px 0 0 white,
        4px -2px 0 white,
        4px -4px 0 white,
        4px -6px 0 white,
        4px -8px 0 white;
        transform: rotate(45deg);
    }

    /*table*/
    #customers {
        font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
        border-collapse: collapse;
        width: 100%;
    }

    #customers td, #customers th {
        border: 1px solid #ddd;
        padding: 8px;
    }

    #customers tr:nth-child(even) {
        background-color: #f2f2f2;
    }

    #customers tr {
        cursor: pointer;
    }

    #customers tr:hover {
        background-color: #ddd;
    }

    #customers th {
        padding-top: 12px;
        padding-bottom: 12px;
        background-color: #f5f5f5;
        text-align: center;
        color: black;
        font-size: 17px;
    }
</style>