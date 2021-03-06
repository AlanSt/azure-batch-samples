# azure-batch-samples
This GitHub repository contains a set of HPC related samples that demonstrate the usage of Microsoft Azure Batch services along with some general purpose utilities. See [http://azure.microsoft.com/en-us/services/batch/](http://azure.microsoft.com/en-us/services/batch/) for more information on the Azure Batch Service.

**Visual Studio Requirements**

You will need VS 2013 or later to compile the projects. If you use VS 2012 or 2010, make sure you have the latest Nuget plugin (2.8 or later) installed. Nuget can be found on  [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).

**Building the Samples**

Download the samples and open the solution file for each one using Visual Studio 2013. Right click on the solution and select "Rebuild". Visual Studio will analyze the dependencies and download the dependent binaries from [nuget.org](http://www.nuget.org/packages/Azure.Batch/).

**Batch Account**

Before you can run any of the samples, you will need an Azure Batch service account. The Azure Batch service is currently in preview; apply for access to the Batch here: [https://account.windowsazure.com/PreviewFeatures](https://account.windowsazure.com/PreviewFeatures).

After obtaining access to the service, you can create a Batch account either on the [Azure.com management portal](https://manage.windowsazure.com) or by using Azure PowerShell to create the account as described at [http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx).

**Notes**

Some of the samples require a pre-created pool with deployed VMs. If your tasks are not being scheduled, it is likely that there are no VMs to host them. You can use Batch Explorer to monitor this situation as well as pre-create the pool and resize it to have some number of VMs.

#CSharp

##[BatchExplorer](./CSharp/BatchExplorer)
Azure Batch Explorer is a GUI application to view and manage Azure Batch Service. See this [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx) for more detail.

##[Helloworld](./CSharp/HelloWorld)
The Helloworld sample is an introduction to the framework required to communicate with the Batch service. It performs some basic list functions as well as creating a pool and a workitem. It also utilizes the task submission helper and task state monitor which, together, provides a simple way of submitting tasks to the service and monitoring their completion. It also demonstrates the use of the FileStaging interface for uploading and downloading files associated with the task. Finally, bulk submission of tasks is demonstrated.

##[ImgProc](./CSharp/ImgProc)
ImgProc demonstrates how to use a single binary that acts both as a client submitting work to the service and as the executable that runs as a task. This particular sample utilizes ImageMagick to convert image files into their associated thumbprint images. More detailed setup instructions are included in this sample's directory.

##[JMScheduling](./CSharp/JMScheduling)
This sample shows how to use a Job Manager task. A JM task is the first task to run in a job and is used to dynamically shape the nature of the work performed during the execution of the job. For example, the JM might choose to submit a different sets of tasks based on the output of tasks that preceded them, etc. This solution has two projects: JMScheduling which calls the Batch service to create the objects needed tostart a job and JobManager which is the actual executable that is run on a VM in the service. It also shows how to upload the Job Manager binaries to a storage account using Azure Storage APIs.

##[TextSearch](./CSharp/TextSearch)
This map-reduce style sample uses Azure Batch to perform parallel text processing on an input file by splitting it up into multiple sub-files and performing regular expression matching on each sub-file. The results are then rolled-up into a final report. This sample also uses a Job Manager to orchestrate the mapper and reducer tasks. It combines all 4 functions into one binary: the submission of the workitem, the job manager, and the mapper and reducer code.

##[TopNWords](./CSharp/TopNWords)
This sample demonstrates how to process a set of input blobs in parallel on multiple VMs. In this case, there is only one blob but the code can be expanded to load more blobs and bind them to individual tasks. The task writes a list of length N to stdout that contains the words in the blob with the highest occurence count. A run-once workitem is created followed by the creation of multiple tasks with each task processing the its blob. The job code then waits for each of the task to complete and then prints out the list generated for each input blob.

#Python

##[blobxfer.py](./Python/Storage)
AzCopy-like helper script to perform large/mass ingress into or egress out of XStore. View the file for details on how to use and customize.
