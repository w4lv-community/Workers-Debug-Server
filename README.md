# Workers Debug Server

The Workers Debug Server is the official debugger for the Workers for LabVIEW development framework. Its purpose is to assist in debugging Workers applications by adding both transparency and access to the running LabVIEW code within a Workers application.
Information about the Workers Debug Server can be found here : [docs.workersforlabview.io/...](https://docs.workersforlabview.io/workers-tools/workers-tools-menu/workers-debug-server)

## Requirements

LabVIEW 2017 or later.  
Workers SDK version 5.0 : download from [vipm.io/package/sc_workers/](https://www.vipm.io/package/sc_workers/)

## Architecture
The Workers 5.0 Debug Server application contains the following Workers, arranged in the following call-chain hierarchy. Each Worker uses the standard Worker APIs for communication between a Worker and its Caller. Thus, communication between Workers exists only up and down the Worker call-chain hierarchy, except where message bypasses are indicated, in which case a message is sent directly from one Worker to another.

![Asset 10](https://github.com/w4lv-community/Workers-Debug-Server/assets/166398268/2b68d7db-f6cd-4a06-b9fe-27051511cc56)

## Workers

The Worker 5.0 Debug Server application contains the following Workers:

### Debug Server
The Head Worker of the application. Facilitates as a message broker for its subWorkers. Manages the application's overall state.

### Application Manager
The Application Manager is the window that first appears when the Debug Server application is loaded. From this window you can access all other exposed Worker front panels (i.e. Settings and Message Logs). Its purpose is to show the call-chain of all running/exited Workers in Workers applications that are connected through the use of Debug Clients to the Debug Server application.

### Message Log
The purpose of the Message Log is to show to users, in real-time, the sequence of messages sent between Workers in a Workers application. This Worker is also able to directly log to file all messages received from a Debug Client. A Message Log Worker can exist for every connected Debug Client.

### Settings
This Worker loads all configuration data for the entire Debug Server application. Here the user may also set and change variables used by the Debug Server application. When the Debug Server application shuts down, the Settings Worker is responsible for collecting data from each Worker and writing it to the application's config file.

### TCP Server
This Worker is responsible for creating a TCP Listener and for spawning TCP Read Workers to asynchronously handle multiple Debug Clients that connect to the Debug Server application.

### TCP Listener
This Worker opens a TCP port and listens continuously for incoming connections from Debug Clients.

### TCP Read
Two TCP Read Workers are spawned for every new connection from a Debug Client. The TCP Read Worker that receives 'LOW' priority data forwards this data (message bypass) to a corresponding Message Log Worker. The TCP Read Worker that receives 'NORMAL' priority data forwards this data (message bypass) directly to the Application Manager Worker.

## Contributing

Contributions are welcome! If you'd like to contribute to the Workers Debug Server, please follow these guidelines:

- Fork the repository.
- Create a new branch for your feature or bug fix.
- Make your changes and ensure that the code passes all tests.
- Submit a pull request with a clear description of your changes.

For more information on contributing, please refer to the [CONTRIBUTING.md](CONTRIBUTING.md) file.


## License

Workers Debug Server is licensed under the [BSD-3 License](https://opensource.org/licenses/BSD-3-Clause). See the [LICENSE](LICENSE) file for details.

## Contact

If you have any questions, suggestions, or issues regarding the Workers Debug Server, please feel free to contact: [workers@scarfecontrols.com](mailto:workers@scarfecontrols).

---

## Disclaimer

The Workers Debug Server is an open-source project and managed by Scarfe Controls. The project is not affiliated with LabVIEW or NI. LabVIEW is a registered trademark of NI.
