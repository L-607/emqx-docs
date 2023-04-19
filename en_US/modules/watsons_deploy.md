# EMQX & Watsons SDES Deploy

## Architecture Design

### Component - EMQX EE cluster

#### Function (3 sections: access, message distribution, data cache)

#### configure (module)

#### Rule engine use (just write MySQL resource configuration, log report persistence rules. Online and offline events have been transferred to the internal implementation of the plug-in)

### Component - BackendAPI (interact with MySQL, provide interface for front end)

### Components - MySQL Database (Introduction Table Structure)

## Architecture Diagram

![sdes_architecture](./assets/sdes/sdes_architecture.png)