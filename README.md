# Daikibo Industrials IIoT Data Integration

## Project Overview
This project addresses the challenge of integrating telemetry data from two different IIoT device formats used by Daikibo Industrials. The goal is to unify these diverse data streams into a single, consistent format for improved monitoring, measurement, and analysis of manufacturing processes.

## How It Works
The solution is implemented in `main.py` and consists of the following key components:

- **`data-1.json` and `data-2.json`**: These files represent the two different input data formats from the IIoT devices. Each file contains a single JSON object with telemetry data.
- **`data-result.json`**: This file defines the target unified format that all incoming telemetry data should conform to.
- **`transform_format_1(entry)`**: A Python function that takes a JSON object from `data-1.json` and transforms it into the unified `data-result.json` format. It handles direct mapping of fields.
- **`transform_format_2(entry)`**: A Python function that takes a JSON object from `data-2.json` and transforms it into the unified `data-result.json` format. This function specifically handles the conversion of ISO 8601 timestamps to milliseconds since epoch, as required by the target format.
- **`main()`**: The main function orchestrates the data integration process. It reads `data-1.json` and `data-2.json`, applies the respective transformation functions, and combines the transformed data into a single list. Finally, it writes this unified data to `output.json`.

## Data Mapping
The following table illustrates the mapping of fields from the source formats to the unified target format:

| `data-1.json` | `data-2.json` | Unified Format (`data-result.json`) |
|---------------|---------------|-------------------------------------|
| `device`      | `id`          | `device_id`                         |
| `time` (ms)   | `timestamp` (ISO) | `timestamp` (ms)                    |
| `temp`        | `temperature_value` | `temperature`                       |
| `press`       | `psi`         | `pressure`                          |
| `status`      | `status`      | `status`                            |

## How to Run
To run this project and generate the unified `output.json` file, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/devv1310/Daikibo_task.git
    ```
2.  **Navigate to the project directory:**
    ```bash
    cd Daikibo_task
    ```
3.  **Execute the main script:**
    ```bash
    python3 main.py
    ```
    This will generate an `output.json` file in the project directory containing the combined and transformed telemetry data.

## Testing
The `main.py` file also includes a `unittest` suite to verify the correctness of the transformation functions. To run the tests:

1.  **Navigate to the project directory:**
    ```bash
    cd Daikibo_task
    ```
2.  **Execute the main script (which runs the tests when executed directly):**
    ```bash
    python3 main.py
    ```
    You should see `OK` if all tests pass, indicating that the data transformations are working as expected.

