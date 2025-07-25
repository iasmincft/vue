<template>
    <Message :msg="msg" v-show="msg" />
    <div id="burger-table-container">
        <table>
            <thead>
                <tr>
                    <th>#:</th>
                    <th>Pedido:</th>
                    <th>Cliente:</th>
                    <th>Pão:</th>
                    <th>Carne:</th>
                    <th>Opcional:</th>
                    <th>Ações:</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="burger in burgers" :key="burger.id">
                    <td>{{ burger.id }}</td>
                    <td>{{ burger.numPedidos }}</td>
                    <td>{{ burger.nome}}</td>
                    <td>{{ burger.pao }}</td>
                    <td>{{ burger.carne}}</td>
                    <td>
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">
                                {{ opcional }}
                            </li>
                        </ul>
                    </td>
                    <td>
                        <select name="status" id="status" @change="updateBurger($event, burger.id, burger.numPedidos)">
                            <option value="">Selecione</option>
                            <option v-for="status in this.status" :key="status.id" :value="status.tipo" :selected="burger.status === status.tipo">
                                {{ status.tipo }}
                            </option>
                        </select>
                        <button class="delete-btn" @click="deleteBurger(burger.id, burger.numPedidos)">Cancelar</button>
                    </td>
                </tr>
                
            </tbody>
        </table>
    </div>
</template>

<script>
import Message from './Message.vue';    

export default {
    name: "Dashboard",
    data () {
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: null
        };
    },
    components: {
        Message
    },
    methods: {
        async getPedidos() {

            const req = await fetch('http://localhost:3000/burgers');

            const data = await req.json();

            this.burgers = data;

            // resgatar status

            this.getStatus();
        },
        async getStatus() {
            // aqui resgatamos os status do backend
            const req = await fetch('http://localhost:3000/status');

            const data = await req.json();

            this.status = data;
        },
        async deleteBurger(id, numPedidos) {
            // aqui deletamos o pedido
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'DELETE'
            });

            const res = await req.json();

            this.msg = `Pedido Nº ${numPedidos} removido com sucesso!`

            this.getPedidos();
        },
        async updateBurger(event, id, numPedidos) {

            const option = event.target.value;

            const dataJson = JSON.stringify({status: option });

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'PATCH',
                headers: {'Content-Type': 'application/json'},
                body: dataJson
            });

            const res = await req.json();

            if (option != "") {
                this.msg = `O pedido Nº ${numPedidos} foi atualizado para ${res.status}!`;

                return;
            } else {
                this.msg = null;
                return;
                
            }
    
        }
    },
    mounted() {
        this.getPedidos();
    }
}
</script>

<style scoped>

#burger-table-container {
    max-width: 1200px;
    margin: 0 auto;
}

table {
    width: 100%;
    border-collapse: collapse;
}

th,
td {
    padding: 12px;
    border-bottom: 1px solid #ccc;
    text-align: left;
}

thead,
th {
    font-weight: bold;
    border-bottom: 3px solid #333;
}

th:first-child,
td:first-child,
td:nth-child(2) {
    width: 5%;
}

td:nth-child(3),
td:nth-child(4),
td:nth-child(5),
td:nth-child(6) {
    width: 19%;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
}

.delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.delete-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>
