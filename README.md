# proccontrol

**proccontrol** is library that makes it easy to build REST based dynamic process controllers. It was developed while building a project at work and it has since found its use in other projects.

## Project Status

Although usable, project is still to be considered as _WORK IN PROGRESS_ until it reaches it's first official version.


## Feature description

- [ ] Start/Stop executables (with or without arguments).
- [ ] Provide activity logs.
- [ ] Provide stats about running session(s).
  - Open sessions
  - Closed sessions
  - Session running time
- [ ] Cron Tasks.

## Installation

You can use _go get_:

    go get -u github.com/sam-ish/proccontrol

## Usage

In order to do any kind of interaction you first need to create an SMPP [Session](https://godoc.org/github.com/sam-ish/smpp#Session). Session is the main carrier of the protocol and enforcer of the specification rules.

Naked session can be created with:

    // You must provide already established connection and configuration struct.
    sess := smpp.NewSession(conn, conf)

But it's much more convenient to use helpers that would do the binding with the remote SMSC and return you session prepared for sending:

    // Bind with remote server by providing config structs.
    sess, err := smpp.BindTRx(sessConf, bindConf)

And once you have the session it can be used for sending PDUs to the binded peer.

    sm := smpp.SubmitSm{
        SourceAddr:      "11111111",
        DestinationAddr: "22222222",
        ShortMessage:    "Hello from SMPP!",
    }
    // Session can then be used for sending PDUs.
    resp, err := sess.Send(p)

Detailed examples for SMPP client and server can be found in the [examples dir](https://github.com/sam-ish/proccontrol/tree/master/examples).
