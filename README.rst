Commit Rules
============

O Commit Rules executa testes para validar o código. Podendo ser utilizado para validar um commit também.

Para usá-lo basta configurar o arquivo ``.commit-rules`` no seu projeto como no exemplo:

.. code-block::

  Git Check: git diff --cached --check
  flake8: flake8


Instalação no Sistema
---------------------

Para instalar o Commit Rules no sistema, basta colocar o arquivo ``commit-rules`` em algum diretório presenta na sua variável ``PATH``, e conseder permissão de execução.

Para verificar os diretórios possívels execute:

.. code-block:: sh

  echo "$PATH" | tr ":" "\n"

Para baixar a última versão presente no repositório do projeto, colocando-o em ``/usr/local/bin``, execute:

.. code-block:: sh

  wget -O "/usr/local/bin/commit-rules" "https://gitlab.com/eduardoklosowski/commit-rules/raw/master/commit-rules"
  chmod +x "/usr/local/bin/commit-rules"


Habilitar a Execução Automática em um Repositório Git
-----------------------------------------------------

O Commit Rules pode ser habilitado para fazer as verificações antes de cada commit, impedindo que commits com erros sejam feitos.

Para configurá-lo desta forma, adicione-o ao Hook ``pre-commit`` do repositório local, exemplo:

.. code-block:: sh

  ln -s /usr/local/bin/commit-rules .git/hooks/pre-commit

Assim os testes serão executados toda vez que um ``git commit`` for feito. Porém ainda é possível não executá-lo com ``git commit --no-verify``.


Configuração
------------

O Commit Rules usa o arquivo ``.commit-rules`` para saber que testes devem ser feitos. A estrutura deste arquivo é em texto plano, formado por um nome para identificar o teste, seguido por seu comando, separados por dois pontos (``:``). Exemplo:

.. code-block::

  Git Check: git diff --cached --check
  flake8: flake8

Neste exemplo dois testes identificados como ``Git Check`` e ``flake8`` serão feitos, executando os comandos ``git diff --cached --check`` e ``flake8`` respectivamente.


Comportamento do Commit Rules
-----------------------------

O executável ``commit-rules`` lê o seu arquivo de configuração, executa os testes, mostrando nome e estádo (``OK`` para sucesso ou ``ERR`` para falha). Quando uma falha é detectada, a saída de seu comando é exibida na tela, e o ``commit-rules`` retorna erro, não executando os demais testes.
