FROM python:3.13-slim

# Install uv.
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Copy the application into the container.
COPY . /app

# Install the application dependencies.
WORKDIR /app
RUN uv sync --frozen --no-cache

# Update system packages and install curl, then clean up to reduce image size
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y curl wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 8001

# Run the application.
CMD ["uv", "run", "/app/weather.py"]
