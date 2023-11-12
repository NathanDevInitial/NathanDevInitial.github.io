
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" type="image/x-icon" href="favicon.ico">
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <title>Calculadora Álgebra Linear</title>
</head>
<body> 
    <div class="container">
    <ul>
        <li><a href="index.html">Página Inicial</a></li>
        <li><a href="calculoGeradorU.html">Calculo Gerador de U</a></li> <!-- Adicione este link -->
        <li><a href="soma_subespacos.html">Soma Subespaços</a></li> <!-- Adicione este link -->
    </ul>


        <label for="vetor_u">Vetor u:</label>
        <input type="text" id="vetor_u">

        <label for="vetor_v">Vetor v:</label>
        <input type="text" id="vetor_v">

        <label for="vetor_w">Vetor w:</label>
        <input type="text" id="vetor_w">

        <button onclick="calcularProdutoEscalar()">Calcular Produto Escalar</button>
        <button onclick="calcularProdutoVetorial()">Calcular Produto Vetorial</button>
        <button onclick="calcularSoma()">Calcular Soma</button>
        <button onclick="calcularInterseccao()">Calcular Interseção</button>
        <button onclick="calcularCombinacaoLinear()">Calcular Combinação Linear</button>
        <button onclick="calcularValorK()">Calcular Valor de k</button>
    </div>

    <script>
       
        function calcularProdutoEscalar() {
            // Obtenha os valores dos vetores do usuário
            var u = $('#vetor_u').val();
            var v = $('#vetor_v').val();
            var w = $('#vetor_w').val();

            // Chame a função Python passando os valores diretamente
            var resultado = calcularProdutoEscalarPython(u, v, w);

            // Manipule o resultado
            alert('Produto Escalar: ' + resultado);
        }

        function calcularProdutoVetorial() {
            var u = $('#vetor_u').val();
            var v = $('#vetor_v').val();
            var w = $('#vetor_w').val();
            var resultado = calcularProdutoVetorialPython(u, v, w);
            alert('Produto Vetorial: ' + resultado);
        }
        

        function calcularInterseccao() {
        var u = $('#vetor_u').val();
        var v = $('#vetor_v').val();
        var w = $('#vetor_w').val();

        $.ajax({
            type: 'POST',
            url: '/calcular',
            contentType: 'application/json;charset=UTF-8',
            data: JSON.stringify({ 'u': u, 'v': v, 'w': w }),
            success: function (data) {
                alert(data.interseccao);
            },
            error: function (error) {
                alert('Erro na requisição AJAX: ' + error.responseText);
            }
        });
    }

        function calcularCombinacaoLinear() {
            var u = $('#vetor_u').val();
            var v = $('#vetor_v').val();
            var w = $('#vetor_w').val();

            $.ajax({
                type: 'POST',
                url: '/calcular',
                contentType: 'application/json;charset=UTF-8',
                data: JSON.stringify({ 'u': u, 'v': v, 'w': w }),
                success: function (data) {
                    alert(data.combinacao_linear);
                },
                error: function (error) {
                    alert('Erro na requisição AJAX: ' + error.responseText);
                }
            });
        }

        function calcularSoma() {
            var u = $('#vetor_u').val();
            var v = $('#vetor_v').val();
            var w = $('#vetor_w').val();

            $.ajax({
                type: 'POST',
                url: '/calcular',
                contentType: 'application/json;charset=UTF-8',
                data: JSON.stringify({ 'u': u, 'v': v, 'w': w }),
                success: function (data) {
                    alert(data.soma);
                },
                error: function (error) {
                    alert('Erro na requisição AJAX: ' + error.responseText);
                }
            });
        }

        function calcularValorK() {
            var u = $('#vetor_u').val();
            var v = $('#vetor_v').val();
            var w = $('#vetor_w').val();

            $.ajax({
                type: 'POST',
                url: '/calcular',
                contentType: 'application/json;charset=UTF-8',
                data: JSON.stringify({ 'u': u, 'v': v, 'w': w }),
                success: function (data) {
                    alert(data.valor_k);
                },
                error: function (error) {
                    alert('Erro na requisição AJAX: ' + error.responseText);
                }
            });
        }

        // Função de exemplo para calcular produto escalar no Python
        function calcularProdutoEscalarPython(u, v, w) {
            // Faça uma requisição AJAX para o servidor Flask
            // A resposta será a string do resultado, não um JSON
            // Isso é um exemplo e você pode precisar ajustar conforme necessário
            return $.ajax({
                type: 'POST',
                url: '/calcular',
                contentType: 'application/json;charset=UTF-8',
                data: JSON.stringify({ 'u': u, 'v': v, 'w': w }),
                async:false,
                success: function(data){
                    alert(data.produto_escalar);
                },
                error: function(error) {
                    alert('Erro na requisição AJAX: ' + error.responseText);
                }
            }).responseText;
        }


        function calcularProdutoVetorialPython(u, v, w) {
            // Faça uma requisição AJAX para o servidor Flask
            // A resposta será a string do resultado, não um JSON
            // Isso é um exemplo e você pode precisar ajustar conforme necessário
            return $.ajax({
                type: 'POST',
                url: '/calcular',
                contentType: 'application/json;charset=UTF-8',
                data: JSON.stringify({ 'u': u, 'v': v, 'w': w }),
                async:false,
                success: function(data){
                    alert(data.produto_vetorial);
                },
                error: function(error) {
                    alert('Erro na requisição AJAX: ' + error.responseText);
                }
            }).responseText;
        }

        function verificarSistemaGerador() {
        // Obtenha os valores dos vetores do usuário
        var u = $('#vetor_u').val();
        var conjuntoVetores = [$('#vetor_v1').val(), $('#vetor_v2').val(), $('#vetor_v3').val()];

        // Chame a função Python passando os valores diretamente
        $.ajax({
            type: 'POST',
            url: '/verificar_sistema_gerador',
            contentType: 'application/json;charset=UTF-8',
            data: JSON.stringify({ 'U': u, 'conjunto_vetores': conjuntoVetores }),
            success: function (data) {
                // Manipule os resultados retornados pelo servidor
                mostrarMensagem(data.mensagem);
                alert('É sistema gerador? ' + (data.resultado ? 'Sim' : 'Não'));
            },
            error: function (error) {
                alert('Erro na requisição AJAX: ' + error.responseText);
            }
        });
    }

        // Defina funções semelhantes para as outras operações

        // ...
    </script>

    <div id="alert"></div>
</body>
</html>
