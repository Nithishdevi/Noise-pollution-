# Noise-pollution-#include <iostream>
#include <vector>
#include <thread>
#include <chrono>
#include <fstream>

// Simulated noise sensor class
class NoiseSensor {
public:
    double getNoiseLevel() {
        // Replace with actual sensor data retrieval
        // You may need to interface with hardware or external libraries.
        return 65.0; // Simulated noise level in dB
    }
};

// Class to log noise data to a file
class NoiseLogger {
public:
    void logNoiseData(double noiseLevel) {
        std::ofstream logFile("noise_log.txt", std::ios::app);
        logFile << "Noise Level: " << noiseLevel << " dB\n";
        logFile.close();
    }
};

// Main noise monitoring function
void monitorNoise() {
    NoiseSensor sensor;
    NoiseLogger logger;
    double noiseThreshold = 60.0; // Adjust the threshold as needed

    while (true) {
        double currentNoiseLevel = sensor.getNoiseLevel();
        logger.logNoiseData(currentNoiseLevel);

        if (currentNoiseLevel > noiseThreshold) {
            std::cout << "Noise pollution detected! Take action." << std::endl;
            // Add code to trigger actions like alerting authorities or soundproofing measures.
        } else {
            std::cout << "Noise pollution within acceptable limits." << std::endl;
        }

        // Sleep for some time before the next reading
        std::this_thread::sleep_for(std::chrono::minutes(1));
    }
}

int main() {
    // Create a separate thread for noise monitoring
    std::thread monitoringThread(monitorNoise);

    // Keep the main thread running to manage the system
    monitoringThread.join();

    return 0;
}
