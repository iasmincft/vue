<template>
    <div id="burger-table-container">
        <table>
            <thead>
                <tr>
                    <th>#:</th>
                    <th>Cliente:</th>
                    <th>Pão:</th>
                    <th>Carne:</th>
                    <th>Opcional:</th>
                    <th>Ações:</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>Iasmin</td>
                    <td>Pão de Trigo</td>
                    <td>Maminha</td>
                    <td>
                        <ul>
                            <li>Bacon</li>
                            <li>Salame</li>
                            <li>Tomate</li>
                        </ul>
                    </td>
                    <td>
                        <select name="status" id="status">
                            <option value="">Status</option>
                        </select>
                        <button class="delete-btn">Cancelar</button>
                    </td>
                </tr>
                
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: "Dashboard",
    data () {
        return {
            burger: null,
            burger_id: null,
            status: []
        };
    },
    methods: {
        async getPedidos() {

            const req = await fetch('http://localhost:3000/burgers');

            const data = await req.json();

            this.burgers = data;

            // resgatar status
            const statusReq = await fetch('http://localhost:3000/status');

            const statusData = await statusReq.json();  
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
td:first-child {
    width: 5%;
}

td:nth-child(2),
td:nth-child(3),
td:nth-child(4),
td:nth-child(5) {
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
