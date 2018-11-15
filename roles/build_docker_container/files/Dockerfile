# Use an official Python runtime as a parent image
FROM python:2.7-slim


# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Copy pip config file
COPY pip.conf /root/.pip/pip.conf

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
ENTRYPOINT ["python"]

CMD ["app.py"]

HEALTHCHECK --interval=2m --timeout=3s \
  CMD curl -f http://localhost/ || exit 1
