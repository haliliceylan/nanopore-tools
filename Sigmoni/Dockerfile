FROM --platform=linux/amd64 haliliceylanua/uncalled4:679e37b as uncalled4
FROM --platform=linux/amd64 oma219/spumoni:v2.0.9 as spumoni

WORKDIR /spumoni

RUN rm -rf build && mkdir build && cd build && cmake .. && make install

FROM --platform=linux/amd64 python:3.11 as build

WORKDIR /app

# RUN apt-get update
# RUN apt-get install -y --no-install-recommends build-essential gcc

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

COPY sigmoni /app

RUN cd src/delta_rust && \
    cargo build --release && \
    mv target/release/libdelta_rust.so ../../delta_rust.so

COPY --chown=user:user --from=uncalled4 /home/user/.local /root/.local

RUN pip install --user numpy pandas scikit-learn Biopython tqdm

RUN find . -type f -name '*.py' -exec sed -i 's/from uncalled/from uncalled4/g; s/import uncalled/import uncalled4/g' {} +



RUN for file in main.py index.py; do \
        chmod +x $file; \
        sed -i '1i #!/usr/local/bin/python' $file; \
    done

FROM --platform=linux/amd64 python:3.11

RUN useradd -m user

# copy uncalled4
COPY --chown=user:user --from=build /root/.local /home/user/.local
ENV PATH=/home/user/.local/bin:$PATH

# copy spumoni
COPY --chown=user:user --from=spumoni /spumoni/build/spumoni /usr/local/bin/spumoni

# copy sigmoni
COPY --chown=user:user --from=build /app /sigmoni
ENV PATH=/sigmoni:$PATH

USER user

WORKDIR /workspace

ENTRYPOINT ["bash"]