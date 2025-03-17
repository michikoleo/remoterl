# Command-Line Interface

The RemoteRL CLI provides a set of commands to interact with the application directly from your terminal. It makes it easy to configure, simulate, train, and deploy your multi‑agent reinforcement learning environments.

## Commands

### Help
Display help information and usage guidelines for RemoteRL CLI commands.
```bash
remoterl --help
remoterl config --help
remoterl simulate --help
...
```

### Config
Update configuration settings that are used by subsequent training or inference commands.

**Basic Configuration:**  
Update global settings such as hyperparameters and AWS Sagemaker setting.
```bash
# Update global configuration with hyperparameters and SageMaker settings
remoterl config --batch_size 256
remoterl config --region us-east-1 --role_arn arn:aws:iam::123456789012:role/AgentGPTSageMakerRole
```

**Advanced Module Configuration:**  
For users who wish to fine-tune or override settings—such as environment hosts, exploration methods, or simulator registry details—the CLI also supports advanced commands.  
> **Note:**  
> In most cases, the simulation command automatically configures environment hosts for you. Advanced users can manually adjust these settings if needed.

```bash
# Configure exploration methods for continuous or discrete control.
remoterl config exploration set continuous --type gaussian_noise
remoterl config exploration set discrete --type epsilon_greedy
remoterl config exploration del discrete
```

**Nested Configuration:**  
Update deeply nested configuration parameters using dot notation for fine-grained control.
```bash
# Change the initial sigma for continuous exploration
remoterl config --exploration.continuous.initial_sigma 0.2 

```

### List
View the current configuration.
```bash
agent-gpt list
```

### Clear
Reset the configuration cache and CLI state.
```bash
remoterl clear
```

### Simulate
Launch simulation environments.  
When you run the `simulate` command, your local machine automatically connects to our RemoteRL WebSocket server on the cloud. This real-time connection enables seamless data communication between your environment's state and the cloud training actions, ensuring that everything is ready for the next remoterl train command.

```bash
# Launch a local gym simulation
remoterl simulate
```

### Train
Initiate a training job on AWS SageMaker.  
This command uses your configuration (including hyperparameters and sagemaker configurations) to submit a training job to the cloud.
```bash
remoterl train
```

---
