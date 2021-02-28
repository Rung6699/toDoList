<template>
    <div id="todoShow">
        <h1 id="headToDo">My to-do list</h1>

        <div id="Box_t"><form @submit.prevent="addOrEditTodo()">
            <label for="topic">Topic:</label>
            <input id="tem_in" type="text" v-model="tempTopic"><br><br><br>
            <label for="detail">Detail:</label>
            <input id="tem_de" type="text" v-model="tempDetail"><br><br><br>
            <label for="date">Date:</label>
            <input id="tem_da" type="date" v-model="tempTime"><br><br><br>
            <label for="time">Time:</label>
            <input id="tem_ti" type="time" v-model="tempDate"><br><br><br>
            <button id="add_t_d" type="submit">Add to-do</button>
        </form>
        </div>

        <div id="return_v" v-for="(todo, index) in showTodo" :key="index">
            <h3>{{todo.topic}}</h3>
            <p>Detail: {{todo.detail}}</p>
            <p>Date: {{todo.date}}</p>
            <p>Time: {{todo.time}}</p>
            <p>Status: {{todo.status}}</p>
            <button id="Re_mo" v-on:click="removeTodo(index)">Remove</button>
            <button id="Ch_mo" v-on:click="toggleState(index)">Check Status</button>
            <button id="E_d" v-on:click="editTodo(index)">Edit</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "todoShow",
        mounted () {
            let retrievedObject = localStorage.getItem('todos')
            console.log(retrievedObject);
            if (retrievedObject !== null) {
                this.todos = JSON.parse(retrievedObject)
            }
        },
        data() {
            return {
                tempTopic: "",
                tempDetail: "",
                tempDate: "",
                tempTime: "",
                todos: [],
                flag: false,
                indexFlag: null
            }
        },
        methods: {
            addOrEditTodo() {
                let temp = {
                    topic: this.tempTopic,
                    detail: this.tempDetail,
                    date: this.tempDate,
                    time: this.tempTime,
                    status: false
                }
                console.log(this.flag)
                if(!this.flag){
                  this.todos.push(temp)
                } else {
                  this.todos[this.indexFlag] = temp
                  this.flag = false
                }
                localStorage.setItem('todos', JSON.stringify(this.todos))
                alert("Add ข้อมูลเรียบร้อย");
            },
            removeTodo(indexToRemove) {
                this.todos.splice(indexToRemove, 1);
                localStorage.setItem('todos', JSON.stringify(this.todos))
            },
            toggleState(index) {
                this.todos[index].status = !this.todos[index].status
                localStorage.setItem('todos', JSON.stringify(this.todos))
            },
            editTodo(index) {
                this.flag = true
                this.indexFlag = index

                this.tempTopic = this.todos[index].topic
                this.tempDetail = this.todos[index].detail
                this.tempDate = this.todos[index].date
                this.tempTime = this.todos[index].time
                alert("เริ่มเเก้ไขข้อมูลที่หน้าหลัก");
            },
        
        },
        computed: {
            showTodo() {
                let tempTodos = this.todos
                return tempTodos
            }
        }
    }
</script>

<style scoped>
#headToDo {
    text-align: center;
    padding: 10px;
}
#todoShow {
    font-size: 20px;
    font-family: Poetsen One;
    color: black;
}
#tem_in {
    border: 3px solid white;
    outline: none;
    border-radius: 10px;
    margin-left: 10px;
}
#tem_de {
    border: 3px solid white;
    outline: none;
    border-radius: 10px;
    margin-left: 10px;
}
#tem_da {
    border: 3px solid white;
    outline: none;
    border-radius: 10px;
    margin-left: 10px;
}
#tem_ti {
    border: 3px solid white;
    outline: none;
    border-radius: 10px;
    margin-left: 10px;
}
#add_t_d {
    border-radius: 30px;
    margin-top: -50px;
    margin-right: 480px;
    width: 150px;
    height: 40px;
    background-color: #C67A34;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
    transition: 0.5s;
    outline: none;
}
#add_t_d:hover {
    outline: none;
    border-radius: 30px;
    margin-top: -50px;
    margin-right: 480px;
    width: 150px;
    height: 40px;
    color: #000000;
    background-color: #ffffff;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
}
#Box_t {
    border: 5px solid #C67A34;
    box-sizing: content-box;
    padding: 20px;
    margin-right: 70%;
    border-radius: 10px;
    background-color: #EABF97;
}
#Re_mo {
    border-radius: 30px;
    width: 150px;
    height: 40px;
    color: white;
    background-color: red;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
    transition: 0.5s;
    outline: none;
}
#Re_mo:hover {
    color: black;
    border-radius: 30px;
    width: 150px;
    height: 40px;
    background-color: #ffffff;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
    transition: 0.5s;
    outline: none;
}
#Ch_mo {
    border-radius: 30px;
    width: 150px;
    margin-left: 5%;
    height: 40px;
    background-color: #C67A34;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
    transition: 0.5s;
    outline: none;
}
#Ch_mo:hover {
    margin-left: 5%;
    border-radius: 30px;
    width: 150px;
    height: 40px;
    background-color: #ffffff;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
    transition: 0.5s;
    outline: none;
}
#E_d {
    margin-left: 1%;
    border-radius: 30px;
    width: 150px;
    height: 40px;
    background-color: #C67A34;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
    transition: 0.5s;
    outline: none;
}
#E_d:hover {
    margin-left: 1%;
    border-radius: 30px;
    width: 150px;
    height: 40px;
    background-color: #ffffff;
    border: #ffffff;
    box-shadow: 0px 12.5216px 10.0172px rgba(0, 0, 0, 0.035), 0px 6.6501px 5.32008px rgba(0, 0, 0, 0.0282725), 0px 2.76726px 2.21381px rgba(0, 0, 0, 0.0196802);
    transition: 0.5s;
    outline: none;
}
</style>