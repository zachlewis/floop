# floop &nbsp; [![Build Status](https://travis-ci.org/d3sw/floop.svg?branch=master)](https://travis-ci.org/d3sw/floop)

Floop is an integration tool which can be used to provide event-based lifecycle data for any process, without requiring any code changes which would couple your application to its consumer. It currently supports integration with STDOUT, HTTP and NATS endpoints, with near-term plans to add additional protocols. 

Integration actions can be configured for the following lifecycle events:
* Begin
* Progress
* Completed
* Failed

## Examples

Floop is currently configured with a single configuration file.  The following example will post JSON to
a single endpoint when the `find` process starts and when it completes.

#### Running Floop

`floop reference_id=1234 -exec find . -name filename`

#### Configuring Floop

```
meta:
  - reference_id

handlers:
  begin:
  - type: http
    uri: "http://my-status-service/${Meta.REFERENCE_ID}"
    options:
      method: "POST"
    body: |
        {
            "status": "started",
        }      
  completed:
  - type: http
    uri: "http://my-status-service/${Meta.REFERENCE_ID}"
    options:
      method: "POST"
    body: |
        {
            "status": "completed",
        }   
```

Additional configuration examples can be found under the [test-data](/test-data) directory.

## Contributing

The purpose of this repository is to continue to evolve floop, adding additional integration protocols
and configuration options.  All development is done publicly on GitHub, and we look forward to working
with a community of both users and developers to make floop even more powerful and intuitive.

Please see the [Contributing Guide](CONTRIBUTING.md) for additional inforamtion on how to open issues 
or submit pull requests.
