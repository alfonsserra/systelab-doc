# Logging

Logs are the stream of aggregated, time-ordered events collected from the output streams of a running process.

Logs in their raw form are typically a text format with one event per line (though backtraces from exceptions may span 
multiple lines). 

Logs have no fixed beginning or end, but flow continuously as long as the app is running.

## Design Considerations

Every technology have their own logging frameworks to manage logs. It is very important to understand how to use 
them as well as to provide specific configurations, to define the messages to be logged as well as for the data format and storage.

An agreement in the frameworks to use, the log formats and information about about how to manage the logs in a 
centralized manner, for example with ELK, it is be priceless.

Finally, it worth to mention that the Twelve-factor applications manifesto tell us to do not attempt to write to or manage logfiles, suggesting that each running process should write its event stream, unbuffered, to stdout.

### Encryption

Log encryption is another popular topic in today's world, because log files often lead to information leaking out, for the information that the files contain and for the fact that usually are saved in plain text.

 
