FROM amazon/aws-lambda-python

# WORKDIR /inference

ARG MODEL_DIR=./models

ENV TRANSFORMERS_CACHE=$MODEL_DIR
ENV TRANSFORMERS_VERBOSITY=error

# RUN yum -y install gcc-c++

COPY requirements.txt requirements.txt
RUN pip install torch==1.10.0+cpu -f https://download.pytorch.org/whl/torch_stable.html
RUN pip install -r requirements.txt

COPY ./ ./

# Run test cases and this saves the transformer model in the container
RUN pip install pytest --no-cache-dir && pytest tests -s -vv

RUN chmod -R 777 ${MODEL_DIR}

CMD [ "main.lambda_handler"]