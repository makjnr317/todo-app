<template>
    <main>
        <div class="tabs">
            <div class="tab" @click="tab = 1">
                All
                <div class="indicator" v-if="tab === 1"></div>
            </div>
            <div class="tab" @click="tab = 2">
                Active
                <div class="indicator" v-if="tab === 2"></div>
            </div>
            <div class="tab" @click="tab = 3">
                Completed
                <div class="indicator"  v-if="tab === 3"></div>
            </div>
        </div>

        <form @submit.prevent="onSubmit" v-if="tab != 3">
            <input type="text" placeholder="add details" name="task" id="task-input" v-model="task">
            <input type="submit" value="Add" :disabled="task===''">
        </form>

        <div class="tasks" :class="{'tab-3-margin': tab === 3 && tasks.length > 0}">
            <div class="task" v-for="task in tasksQuery" :key="task">
                <div>
                    <input type="checkbox" v-model="task.completed">
                    <p class="task-title" :class="{completed: task.completed}">
                        {{task.task}}
                    </p>
                </div>
                <span class="material-icons-outlined delete" v-if="tab === 3" @click="del(task)">delete</span>
            </div>

            <div class="delete-button" v-if="tab===3" @click="deleteAll">
                <span class="material-icons-outlined delete-button-icon">delete</span>
                delete all
            </div>

        </div>
    </main>
</template>

<script>
export default {
    data(){
        return{
            task: '',
            tab: 1,
            tasks: [],
        }
    },
    methods:{
        onSubmit(){
            this.tasks.push({task:this.task, completed:false})
            this.task=""
        },
        deleteAll(){
            this.tasks = []
        },
        del(task){
            this.tasks = this.tasks.filter(x => x != task)
        }
    },
    computed:{
        tasksQuery(){
            if (this.tab === 1){
                return this.tasks
            }
            if (this.tab ===2){
                return this.tasks.filter(x => !x.completed)
            }
            else{
                return this.tasks.filter(x => x.completed)
            }
        }
    }
}
</script>

<style>
main{
    display: flex;
    flex-direction: column;
    align-items: center;

}

.tabs{
    display: flex;
    padding: 0 66px 0 66px;
    justify-content: space-between;
    padding-bottom: 19px;
    border-bottom: 1px solid #BDBDBD;
    text-align: center;
    width: 100%;
    max-width: 608px;
}

.tab{
    font-weight: 600;
    width: 89px;
    font-size: 14px;
    color: #333333;
}

form{
    margin: 18px 0 32px 0;
    width: 608px;
    display: flex;
    width: 100%;
    max-width: 608px;
}

input[type='checkbox']{
    height: 24px;
    width: 24px;
}

input[type='submit']{
    color: #fff;
    font-weight: 600;
    font-size: 14px;
    border: none;
    padding: 20px 40px;
    background: #2F80ED;
    box-shadow: 0px 2px 6px rgba(127, 177, 243, 0.4);
    border-radius: 12px;
    margin-left: 25px;
}

#task-input{
    padding: 19px 12px;
    font-size: 14px;
    border: 1px solid #BDBDBD;
    box-sizing: border-box;
    border-radius: 12px;
    width: 476px;
}

.task-title{
    font-weight: 500;
    font-size: 18px;
    color: #000000;
    display: inline;
    margin-left: 7px;
}

.task{
    display: flex;
    justify-content: space-between;
}

.task>div{
    display: flex;
    align-items: center;
}

.tasks{
    width: 100%;
    max-width: 608px;
    padding-bottom: 40px;
}

.completed{
    text-decoration: line-through;
    color: #333333;
    text-decoration-color: #333333;
}

.tasks>.task:not(:last-child){
    margin-bottom: 27px;
}

.indicator{
    width: 89px;
    height: 4px;
    background: #2F80ED;
    border-radius: 4px 4px 0px 0px;
    position: relative;
    bottom: -19px;
}

.delete{
    color: #BDBDBD;
}

.delete-button{
    width: 124px;
    height: 40px;
    background: #EB5757;
    border-radius: 4px;
    font-weight: 600;
    font-size: 12px;
    color: #FFFFFF;
    display: flex;
    align-items: center;
    justify-content: center;
    float: right;
    margin-top: 32px;
}

.delete-button-icon{
    transform: scale(0.75);
}

.tab-3-margin{
    margin-top: 19px;
}

@media screen and (max-width:690px){
    #app{
        padding: calc(16px + 1vw) calc(20px + 1vw) 0 calc(20px + 1vw) !important;
    }

    .task-title{
        font-size: calc(13px + 1vw);
    }

    input[type='checkbox']{
        height: calc(16px + 1vw);
        width: calc(16px + 1vw);
    }

    .tabs{
        padding: 0 calc(48px + 1vw) 16px calc(48px + 1vw);
    }

    .tasks>.task:not(:last-child){
        margin-bottom: 22px;
    }
}

@media screen and (max-width:575px){
    .tabs{
        padding: 0 calc(30px + 1vw) 16px calc(30px + 1vw);
    }

    .tasks>.task:not(:last-child){
        margin-bottom: calc(14px + 1vw);
    }
}

@media screen and (max-width:425px){
    .tabs{
        padding: 0 calc(15px + 1vw) 16px calc(15px + 1vw);
    }

    form{
        flex-direction: column;
    }

    input[type='submit']{
        margin:16px 0 0 0 ;
        padding: 14px 0;
    }
    
    #task-input{
        width: unset;
        padding: 14px 8px;
    }
}
</style>