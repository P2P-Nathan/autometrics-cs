# Autometrics for .NET

Autometrics-CS is a C# instrumentation of the [Autometrics](https://github.com/autometrics-dev) observability micro-framework. It makes it quick and easy to instrument your code to collect standardized metrics, including function call counts, durations, and build information. This project includes a sample application which shows examples for generating metrics to the console, Prometheus, or hosting and endpoint for scraping.

## Aspect-Oriented Programming and AspectInjector

Autometrics-CS utilizes Aspect-Oriented Programming (AOP) techniques to provide non-invasive and modular instrumentation. AOP allows you to inject additional behavior (in our case, metrics collection) into your methods without altering the original code. This project uses the [AspectInjector](https://github.com/pamidur/aspect-injector) library to achieve AOP in C#.

## Getting Started

To get started with Autometrics, follow these steps:

1. Clone the repository: `git clone https://github.com/autometrics-dev/autometrics.git`
2. Open the solution in Visual Studio or your preferred C# IDE.
3. Build the solution and add a reference to the Autometrics library in your project.

## Examples

Check out the `Autometrics.Samples` project for examples of how to use Autometrics in your code.  Additional information on how this works and using if for testing is on the [Testing Notes](TestingNotes.md) page.

## Usage

To use Autometrics, follow these steps:

1. Import the Autometrics package and its dependencies in your code.
2. Add the `[Autometrics]` attribute to the methods you want to instrument.
3. Configure the desired destination

## Example

Here's an example of how to instrument Autometrics in a C# Console application and export the metrics to the OpenTelemetry collector.

```csharp
using Autometrics.Instrumentation.Attributes;
using OpenTelemetry;

namespace MyProject
{
    class Program
    {
        [Autometrics]
        public static void MyInstrumentedMethod()
        {
            // Your code here
        }

        static void Main(string[] args)
        {

            // Create a meter provider with the Otlp exporter connected to the Autometrics.Instrumentation
            using var meterProvider = Sdk.CreateMeterProviderBuilder()
                .AddMeter("Autometrics.Instrumentation")
                .AddOtlpExporter()
                .Build();

            // Call your instrumented method(s)
            MyInstrumentedMethod();
        }
    }
}
```

## Running the Sample Application and looking at the Grafana Dashboards

Running the application generates a steady flow of activity with the ocassional error
![image](https://user-images.githubusercontent.com/17866458/236915271-244170f4-1345-4817-8b5c-84e70d715339.png)

The pre-build Grafana Dashboards display the activity the same as all over Autometrics projects 
![image](https://user-images.githubusercontent.com/17866458/236915571-f20dfb9e-7639-4406-80f3-34ca1315d25c.png)
![image](https://user-images.githubusercontent.com/17866458/236916166-2a387d96-de70-405e-bdb6-f54faa98545d.png)






