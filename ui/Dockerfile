FROM python:3.12-slim

ENV PYTHONUNBUFFERED=1 \
    PATH="/opt/venv/bin:$PATH" \
    PORT=8080

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential curl && rm -rf /var/lib/apt/lists/*

RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

WORKDIR /app

# Install Python dependencies for the UI
COPY ui/requirements.txt /app/requirements.txt
RUN pip install --upgrade pip
RUN pip install -r /app/requirements.txt

# Copy UI sources
COPY ui/ /app/ui
COPY . .

EXPOSE $PORT

# Start Streamlit on the port Cloud Run provides
CMD ["sh", "-c", "streamlit run ui/streamlit_app.py --server.port $PORT --server.address 0.0.0.0 --server.headless true"]
