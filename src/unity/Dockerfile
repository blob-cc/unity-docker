# syntax=docker/dockerfile:1.4

# Base Image
# =============================================================================
# Use a specific Unity version from UnityCI
FROM unityci/editor:2020.3.11f1-base-0.14.0

# System Dependencies
# =============================================================================
# Install essential packages and clean up to reduce image size
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    git \
    ca-certificates \
    unzip \
    vim \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Set up a non-root user to run the container more securely
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update && apt-get install -y sudo \
    && echo $USERNAME ALL=\(ALL\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Environment Variables
# =============================================================================
# Define necessary environment variables
ENV UNITY_LICENSE_FILE=/root/.local/share/unity3d/Unity/Unity_lic.ulf
ENV DEBIAN_FRONTEND=noninteractive

# Set the user to the non-root user
USER $USERNAME

# Working Directory
# =============================================================================
# Set the working directory
WORKDIR /workspace

# Optional: Copy the license file or other required files from host
# COPY path/to/Unity_lic.ulf $UNITY_LICENSE_FILE

# Container Startup Configuration
# =============================================================================
# Optional: Define an entrypoint or command for the container startup
# ENTRYPOINT ["your-entrypoint-script.sh"]
# CMD ["your-command"]