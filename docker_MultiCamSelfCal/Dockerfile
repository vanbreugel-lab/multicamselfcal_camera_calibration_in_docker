# octave in container
FROM gnuoctave/octave:4.0.0

# non-interactive mode for automated installations
ARG DEBIAN_FRONTEND=noninteractive

# working directory in container
WORKDIR /home

RUN apt update && \
    apt upgrade -y && \
    apt install git -y && \
    git clone https://github.com/strawlab/MultiCamSelfCal.git && \
    cd MultiCamSelfCal && \
    git checkout 94e0bb2a479546d0af6bf29a3681aae7be08daf9 
