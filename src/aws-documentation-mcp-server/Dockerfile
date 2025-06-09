# Python 3.12 のスリムイメージをベースに使用
FROM python:3.12-slim-bookworm

# uv (高速インストーラー) をインストール
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# 作業ディレクトリを作成
WORKDIR /app

# アプリケーションのファイルをコピー
# 注意: このDockerfileはサーバーのソースコードと同じディレクトリに配置してください
COPY ./pyproject.toml ./

# 依存関係をインストール
RUN uv pip install "awslabs-aws-documentation-mcp-server @ git+https://github.com/awslabs/mcp.git#subdirectory=src/aws-documentation-mcp-server"

# サーバーがリッスンするポートを公開
EXPOSE 9712

# 環境変数を設定
ENV FASTMCP_LOG_LEVEL=INFO

# コンテナ起動時にサーバーを実行
ENTRYPOINT ["uv", "run", "aws-documentation-mcp-server"]