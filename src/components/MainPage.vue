<template>
    <div class="mainarea">
        <div class="addplayer">
            <button @click="activatedtag = !activatedtag" class="activated">Oyuncu eklemek istermisiniz?</button>
            <div v-if="activatedtag" class="traits">
                <label for="name">İSİM</label>
                <input id="name" type="text">
                <label for="İD">ID</label>
                <input id="ID" type="number">
                <button @click="addplayers" class="admitted">EKLE</button>
            </div>
        </div>
        <hr>
        <hr>
        <div class="team">
            <p>TEAM A</p>
            <div class="field" draggable="true">
                <draggable class="dragg" :list="list2" group="{ name: 'mygroup', pull: true, put: true }"
                    @end="handleDragEnd">
                    <div class="playerb dragarea1" v-for="element in list2" :key="element.id">
                        <img @click="approve = !approve" class="res"
                            :src="'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQfBMD6ujjGhaX5JfpiuvhJgDthBrgzk8cDWw&usqp=CAU'"
                            alt="">
                        <p>{{ element.name }}</p>
                        <button @click="deleted(element.id)" class="admitted">DELETE</button>
                        <hr>
                        <div v-if="approve" id="pop">
                            <label for="newname">YENİ İSİM</label>
                            <input id="newname" type="text" v-model="newname" >
                            <button @click="handleElementClick(element.id)" class="update" id="approve">UPDATE</button>
                        </div>
                    </div>
                </draggable>
                <hr>
                <hr>

                <draggable class="dragg" :list="list4" group="{ name: 'mygroup', pull: true, put: true }"
                    @end="handleDragEnd">
                    <div class="playerb dragarea1" v-for="element in list4" :key="element.id">
                        <img class="res"
                            :src="'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQfBMD6ujjGhaX5JfpiuvhJgDthBrgzk8cDWw&usqp=CAU'"
                            alt="">
                        <p>{{ element.name }}</p>
                    </div>
                </draggable>
            </div>
        </div>

        <div class="team">
            <p>TEAM B</p>
            <div class="field">
                <draggable class="dragg" :list="list" group="{ name: 'mygroup', pull: true, put: true }"
                    @end="handleDragEnd">
                    <div class="playerb dragarea1" v-for="element in list" :key="element.id">
                        <img class="res"
                            :src="'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQfBMD6ujjGhaX5JfpiuvhJgDthBrgzk8cDWw&usqp=CAU'"
                            alt="">
                        <p>{{ element.name }}</p>
                    </div>
                </draggable>
                <hr>
                <hr>
                <draggable class="dragg" :list="list3" group="{ name: 'mygroup', pull: true, put: true }"
                    @end="handleDragEnd">
                    <div class="playerb dragarea1" v-for="element in list3" :key="element.id">
                        <img class="res"
                            :src="'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQfBMD6ujjGhaX5JfpiuvhJgDthBrgzk8cDWw&usqp=CAU'"
                            alt="">
                        <p>{{ element.name }}</p>
                    </div>
                </draggable>

            </div>
        </div>

    </div>
</template>

<script>
import { VueDraggableNext } from 'vue-draggable-next'
export default {
    name: "MainPage",
    components: {
        draggable: VueDraggableNext
    },
    data() {
        return {
            list: [
                { name: 'John', id: 1 },
                { name: 'Joao', id: 2 },
                { name: 'Jean', id: 3 },
                { name: 'Gerard', id: 4 }
            ],
            list2: [
                { name: 'John', id: 5 },
                { name: 'Joao', id: 6 },
                { name: 'Jean', id: 7 },
                { name: 'Gerard', id: 8 }
            ],
            list3: [
                { name: 'John', id: 9 },
                { name: 'Joao', id: 10 },
                { name: 'Jean', id: 11 }
            ],
            list4: [],
            activatedtag: true,
            approve: false,
            newname: ''
        }
    },
    methods: {
        handleDragEnd() {
            // Drag işlemi bittiğinde, list2'nin güncel uzunluğunu kontrol edebilirsiniz
            console.log('Drag işlemi bitti. Eleman sayısı:', this.list2.length);
        },
        addplayers() {

            var name = document.getElementById('name');
            var ID = document.getElementById('ID');

            this.list4.push({
                name: name.value,
                id: ID.value
            })


            document.getElementById('name').value = "";
            document.getElementById('ID').value = "";
        },
        handleElementClick(id) {
            var name = document.getElementById('newname').value;
            const index = this.list2.findIndex(item => item.id === id);


            if (index !== -1) {
                // Yeni bir değer atayabilirsiniz, örneğin:
                this.list2[index].name = this.newname;
                this.approve = false;
                this.newname = '';
            }

            console.log(name)



        },
        deleted(id) {
            const index = this.list2.findIndex(item => item.id === id);


            if (index !== -1) {

                this.list2.splice(index, 1);
            }

        },

    }
}
</script>

<style  scoped>
.mainarea {
    display: flexbox;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: space-between;
    align-items: center;
    margin: 10px;
    padding: 25px;
    background-color: blue;
    width: auto;
    height: 100vh;
    max-height: fit-content;
}

.team {
    display: flexbox;
    justify-content: space-between;
    align-items: center;
    flex-direction: row;
    margin: 10px;
    padding: 25px;
    width: 45%;
    height: auto;
    float: left;
    background-color: red;
}

p {
    color: white;
    font-size: 20px;
    text-align: center;
    margin: 0;
    padding: 0;

}

.field {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: flex-start;
    margin: 10px;
    margin-top: 50px;
    padding: 25px;
    width: calc(100%-25px);
    height: 100vh;
    background-color: green;
}

.res {
    width: 100px;
    height: 100px;
}

.player {
    display: flex;
    justify-content: center;
    flex-direction: column;
    flex-wrap: nowrap;
    margin: 10px;
    padding: 15px;
}

.inp {
    color: black;
    margin: 0;
    padding: 0;

}

.playerb {
    padding: 15px;
    margin: 10px;
    width: auto;
    height: auto;
    background-color: cadetblue;
    align-items: center;
    text-align: center;
}

.dragarea1 {
    display: flexbox;
    justify-content: space-between;
    align-items: center;
    flex-direction: row;
    flex-wrap: wrap;
}

.dragg {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: row;
    flex-wrap: nowrap;
    width: 100%;
    height: auto;
    margin-top: 20px;
}

.addplayer {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
}

.activated {
    background-color: #4caf50;
    color: #fff;
    padding: 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.traits {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

label {
    margin-bottom: 5px;
}

input {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    box-sizing: border-box;
}

.admitted {
    background-color: #2196f3;
    color: #fff;
    padding: 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.popup {
    display: none;
    position: absolute;
    height: 100vh;
    width: 100vw;
    background-color: #2196f3;
    z-index: 11111;
}
</style>