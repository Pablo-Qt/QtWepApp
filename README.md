# QtWepApp
[QtWepApp](http://stefanfrings.de/qtwebapp/index-en.html) is a HTTP server library in C++, inspired by Java Servlets. 

For Linux, Windows, Mac OS and many other operating systems that the [Qt Framework](http://qt.io/) supports.

QtWebApp contains the following components

* HTTP Server
* Template Engine
* File Logger
* Windows Service Installer

These components can be used independently of each other.
The HTTP server processes incoming requests in parallel threads. It supports IPv4 and IPv6, persistent connections, HTTPS, session cookies, and file-uploads.

The template engine is helpful to generate websites which are based on template files by filling placeholders with data. It supports many languages and may be used for any text based file format (e.g. HTML, XML, CSV, ...). Other larger template engines, such as ClearSilver, may be used as well.

The logger plugs into Qt and writes log messages into files, while they are enriched with additional attributes like timestamp, thread ID, session ID and some more. Changes to the configuration file of the logger become active automatically without program restart. A ring-buffer adds details with debug level to error messages, without the need to output them permanently.

The QtService component enables you to set up your application as a Windows Service.

The small memory requirement of about 2MB qualifies the web server to be used in embedded systems. For example the [Beer brewing machine](http://sebastian-duell.de/en/mashberry/index.html) of Sebastian Düll. But it's also powerful enough for larger web services.

A very small example:
  
    // The request handler receives and responds HTTP requests
    void MyRequestHandler\:\:service\(HttpRequest\& request\, HttpResponse\& response\)
    {
      // Get a request parameters
      QByteArray username=request.getParameter("username");
    
      // Set a response header
      response.setHeader("Content-Type", "text/html; charset=ISO-8859-1");
    
      // Generate the HTML document
      response.write("<html><body>");
      response.write("Hello ");
      response.write(username);
      response.write("</body></html>");
    }
  
    // The main program starts the HTTP server
    int main(int argc, char *argv[])
    {
      QCoreApplication app(argc,argv);
          
      new HttpListener(
          new QSettings("configfile.ini",QSettings::IniFormat,&app),
          new MyRequestHandler(&app),
          &app);
  
      return app.exec();
    }
  
You may download QtWebApp.zip for free and use the software under the conditions of the [LGPL License](http://www.gnu.org/licenses/lgpl.html). The [Tutorial](http://stefanfrings.de/qtwebapp/tutorial/index.html) explains how to use the library. And here is the [API documentation](http://stefanfrings.de/qtwebapp/api/index.html).

Thanks
------
The current high quality of the library is the result of the collaboration of many people. I would like to thank the helpers for testing QtWebApp extensively in a productive environment and thus contributing to the improvement.

Version
-------
從版本 1.7.11 28.12.2019 複製過來的
