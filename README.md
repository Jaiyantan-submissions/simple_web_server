# EX01 Developing a Simple Webserver

# Date: 13/09/24
# AIM:
To develop a simple webserver to serve html pages and display the configuration details of laptop.

# DESIGN STEPS:
## Step 1:
HTML content creation.

## Step 2:
Design of webserver workflow.

## Step 3:
Implementation using Python code.

## Step 4:
Serving the HTML pages.

## Step 5:
Testing the webserver.

# PROGRAM:

# web.py:

    from http.server import HTTPServer,BaseHTTPRequestHandler
    content = """
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Laptop Configuration</title>
            <style>
            
                @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

                
                body {
                    font-family: 'Roboto', Arial, sans-serif;
                    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364); 
                    background-size: 400% 400%;
                    animation: gradientShift 15s ease infinite; 
                    color: #e0e0e0;
                    margin: 0;
                    padding: 0;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    height: 100vh;
                }

            
                @keyframes gradientShift {
                    0% { background-position: 0% 50%; }
                    50% { background-position: 100% 50%; }
                    100% { background-position: 0% 50%; }
                }

                
                .container {
                    background: rgba(18, 18, 18, 0.9); 
                    border-radius: 12px;
                    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7); 
                    padding: 40px 50px;
                    max-width: 800px;
                    width: 90%;
                    position: relative;
                    transition: transform 0.3s ease, box-shadow 0.3s ease;
                }
                .container:hover {
                    transform: translateY(-5px);
                    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.9);
                }


                h1 {
                    font-size: 28px;
                    margin-bottom: 20px;
                    text-align: center;
                    color: #00bcd4; 
                    border-bottom: 2px solid #00bcd4;
                    display: inline-block;
                    padding-bottom: 8px;
                    text-transform: uppercase;
                    letter-spacing: 1.2px;
                }

                
                table {
                    width: 100%;
                    border-collapse: collapse;
                    margin-top: 20px;
                }
                th, td {
                    text-align: left;
                    padding: 15px 20px;
                    border-bottom: 1px solid #444;
                }
                th {
                    background-color: #1e272e; 
                    color: #00bcd4; 
                    font-weight: 600;
                    text-transform: uppercase;
                }
                tr:nth-child(even) {
                    background-color: #121212; 
                }
                tr:hover {
                    background-color: #1e1e1e; 
                }
                td {
                    font-size: 15px;
                    color: #ddd; 
                }
                th:first-child, td:first-child {
                    border-radius: 8px 0 0 8px;
                }
                th:last-child, td:last-child {
                    border-radius: 0 8px 8px 0;
                }
                .footer {
                    text-align: center;
                    margin-top: 20px;
                    font-size: 12px;
                    color: #ec2323;
                }
            </style>
        </head>
        <body>
            <div class="container">

                <h1>Laptop Configuration Details</h1>    
                <table>
                    <thead>
                        <tr>
                            <th>Property</th>
                            <th>Value</th>
                        </tr>
                    </thead>
                    <tbody>
                        {% for key, value in config.items %}
                        <tr>
                            <td>{{ key }}</td>
                            <td>{{ value }}</td>
                        </tr>
                        {% endfor %}
                    </tbody>
                </table>
            </div>

            
            <div class="footer">
                © 2024 Laptop Configurations. Crafted for 6LI-1 Web Assingment.
            </div>
        </body>
        </html>
    """
    class myhandler(BaseHTTPRequestHandler):  
        def do_GET(self):
            print("request received")
            self.send_response(200)
            self.send_header('content-type', 'text/html; charset=utf-8')
            self.end_headers()
            self.wfile.write(content.encode())
    server_address =('',8000)
    httpd=HTTPServer(server_address,myhandler)
    print("my webserver is running...")
    httpd.serve_forever()

    
# OUTPUT:
![Result pic](image1.png)
![Result pic](output1.png)


# RESULT:
The program for implementing simple webserver is executed successfully.
