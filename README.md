# Real Estate Price Prediction Project :house_with_garden: :moneybag:

This data science project series walks through the step-by-step process of building a real estate price prediction website. We will use the Bangalore home prices dataset from Kaggle.com to build a model using sklearn and linear regression. Additionally, we will create a Python Flask server to serve HTTP requests and a website built in HTML, CSS, and JavaScript to allow users to enter home square footage, number of bedrooms, etc., and retrieve the predicted price through the Flask server.

## Project Overview :clipboard:

During model building, we will cover various data science concepts, including data loading and cleaning, outlier detection and removal, feature engineering, dimensionality reduction, gridsearchcv for hyperparameter tuning, k-fold cross-validation, and more. The technology and tools used in this project include:

- Python
- Numpy and Pandas for data cleaning
- Matplotlib for data visualization
- Sklearn for model building
- Jupyter Notebook, Visual Studio Code, and PyCharm as IDEs
- Python Flask for HTTP server
- HTML/CSS/JavaScript for UI
- Deployment on AWS EC2 cloud

## AWS EC2 Setup :cloud: :electric_plug:

To deploy this app to the cloud (AWS EC2), follow these steps:

1. Create an EC2 instance using the Amazon console.
2. In the security group, add a rule to allow HTTP incoming traffic.
3. Connect to your instance using a command like this:
   ```bash
   ssh -i "C:\Users\Viral\.ssh\Banglore.pem" ubuntu@ec2-3-133-88-210.us-east-2.compute.amazonaws.com
   ```

## Nginx Setup :gear: :globe_with_meridians:

Install and configure Nginx on your EC2 instance with the following commands:

```bash
sudo apt-get update
sudo apt-get install nginx
sudo service nginx status  # Check status of Nginx
```

Use the following commands to manage Nginx:

```bash
sudo service nginx start    # Start Nginx
sudo service nginx stop     # Stop Nginx
sudo service nginx restart  # Restart Nginx
```

After setting up Nginx, you will see a "welcome to nginx" message when you load your cloud URL in the browser.

## Code Deployment :rocket:

1. Copy all your project code files into the `/home/ubuntu/BangloreHomePrices` folder on your EC2 instance. You can use Git or WinSCP for this purpose.
2. Create the Nginx configuration file `bhp.conf` in `/etc/nginx/sites-available` with the following content:

```nginx
server {
    listen 80;
    server_name bhp;
    root /home/ubuntu/BangloreHomePrices/client;
    index app.html;
    location /api/ {
        rewrite ^/api(.*) $1 break;
        proxy_pass http://127.0.0.1:5000;
    }
}
```

3. Create a symlink for this file in `/etc/nginx/sites-enabled` with the following command:

```bash
sudo ln -v -s /etc/nginx/sites-available/bhp.conf
```

4. Remove the symlink for the default file in `/etc/nginx/sites-enabled` directory:

```bash
sudo unlink default
```

5. Restart Nginx to apply the changes:

```bash
sudo service nginx restart
```

## Flask Server Setup :snake: :computer:

1. Install Python packages and start the Flask server:

```bash
sudo apt-get install python3-pip
sudo pip3 install -r /home/ubuntu/BangloreHomePrices/server/requirements.txt
python3 /home/ubuntu/BangloreHomePrices/client/server.py
```

Running the last command will prompt that the server is running on port 5000.

## Accessing the Website :earth_americas:

Now, simply load your cloud URL in the browser (e.g., http://ec2-3-133-88-210.us-east-2.compute.amazonaws.com/) to access the fully functional real estate price prediction website running in a production cloud environment. Enjoy! :tada:

For more details, check out the code and the project walkthrough in the Jupyter Notebooks provided.

**Happy Predicting!** :chart_with_upwards_trend: :house:
