FROM ubuntu:22.04

# Install Python and pip
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements and install
#COPY requirements.txt /tmp/
#RUN pip install -r /tmp/requirements.txt
RUN pip install mkdocs mkdocs-material mkdocs-macros-plugin mkdocs-section-index pyyaml

