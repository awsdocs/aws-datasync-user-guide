# Filtering data transferred by AWS DataSync<a name="filtering"></a>

AWS DataSync lets you apply filters if you only want to transfer a subset of data \(such as specific files, folders, or objects\)\.

For example, if your source location includes temporary files that end with `.tmp`, you can create an exclude filter that keeps these files from making their way to the destination location\. You also can use a combination of exclude and include filters in the same task\.

**Topics**
+ [Filtering terms, definitions, and syntax](#filter-overview)
+ [Excluding data from a transfer](#exclude-filters)
+ [Including data in a transfer](#include-filters)
+ [Example filters](#sample-filters)

## Filtering terms, definitions, and syntax<a name="filter-overview"></a>

These are some terms and definitions for use with filtering:

**Filter **  
The whole string that makes up a particular filter, for example: `*.tmp``|``*.temp` or `/folderA|/folderB`  
Filters are made up of patterns delimited with a \| \(pipe\)\. A delimiter isn't needed when you add patterns on the console because you add each pattern separately\.

**Pattern**  
 A pattern within a filter\. For example, `*.tmp` is a pattern that's part of the `*.tmp``|``*.temp` filter\.

**Folders**  
+ All filters are relative to the source location path\. For example, suppose that you specify `/my_source/` as the source path when you create your source location and task and specify the include filter `/transfer_this/`\. In this case, DataSync transfers only the directory `/my_source/transfer_this/` and its contents\.
+ To specify a folder directly under the source location, include a forward slash \(/\) in front of the folder name\. In the example preceding, the pattern uses `/transfer_this`, not `transfer_this`\.
+ DataSync interprets the following patterns the same way and matches both the folder and its content\.

  `/dir` 

  `/dir/`
+ When you are transferring data from or to an Amazon S3 bucket, DataSync treats the / character in the object key as the equivalent of a folder on a file system\.

**Special characters**  
Following are special characters for use with filtering\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/datasync/latest/userguide/filtering.html)

## Excluding data from a transfer<a name="exclude-filters"></a>

*Exclude filters* define files, folders, and objects that are excluded when you transfer files from a source to a destination location\. You can configure these filters when you create, edit, or start a task\.

To create a task with an exclude filter in the DataSync console, specify a list of patterns in the **Data transfer configuration** section under **Exclude patterns**\. For example, to exclude the temporary folders named `temp` or `tmp`, you can specify `*/temp` in the **Exclude patterns** text box, choose **Add patterns** and then specify `*/tmp` in the second text box\. To add more patterns to the filter, choose **Add pattern**\. When you're using the AWS Command Line Interface \(AWS CLI\), single quotation marks \(`'`\) are required around the filter and a \| \(pipe\) is used as a delimiter\. For this example, you would specify `'*/temp`\|`*/tmp'`\.

After you have created a task, you can edit the task configuration to add or remove patterns from the exclude filter\. Your changes are applied to future executions of the task\.

When you run a task, you can modify the exclude filter patterns by using the **Start with overrides** option\. Any changes that you make are applied only to that execution of the task\.

You can also use the AWS CLI to create or edit an exclude filter\. The following example shows such a CLI command\.

```
aws datasync create-task 
    --source-location-arn 'arn:aws:datasync:region:account-id:location/location-id'
    --destination-location-arn 'arn:aws:datasync:region:account-id:location/location-id'
    --cloud-watch-log-group-arn 'arn:aws:logs:region:account-id:log-group:your-log-group' 
    --name your-task-name
    --excludes FilterType=SIMPLE_PATTERN,Value='*/temp|*/tmp'
```

**Note**  
If you are migrating files from a NetApp system, we recommend that you exclude NetApp backup folders by specifying `*/.snapshot` as a pattern in your exclude filter\.

## Including data in a transfer<a name="include-filters"></a>

*Include filters* define files, folders, and objects that DataSync transfers when you run a task\. You can configure include filters when you create, edit, or start a task\.

To create a task with an include filter, choose the **Specific files and folders** option, and then specify a list of patterns to include under **Include patterns**\.

DataSync scans and transfers only files and folders that match the include filters\. For example, to include a subset of your source folders, you might specify `/important_folder_1`\|`/important_folder_2`\. 

After you have created a task, you can edit the task configuration to add or remove patterns from the include filter\. Any changes that you make are applied to future executions of the task\.

When you run a task, you can modify the include filter patterns by using the **Start with overrides** option\. Any changes that you make are applied only to that execution of the task\.

You can also use the AWS CLI to create or edit an include filter\. The following example shows the CLI command\. Take note of the quotation marks \(`'`\) around the filter and the `|` \(pipe\) that's used as a delimiter\.

```
aws datasync start-task-execution 
   --task-arn 'arn:aws:datasync:region:account-id:task/task-id' 
   --includes FilterType=SIMPLE_PATTERN,Value='/important_folder1|/important_folder2'
```

**Note**  
Include filters support the wildcard \(\*\) character only as the rightmost character in a pattern\. For example, `/documents*`\|`/code*` is supported, but `*.txt` isn't supported\.

## Example filters<a name="sample-filters"></a>

The following examples show common filters you can use with DataSync\.

**Note**  
When creating your own filters, make sure you know the [Task filter quotas](datasync-limits.md#filter-limits)\.

**Exclude some folders from your source location**  
In some cases, you might exclude folders in your source location to not copy them to your destination location\. For example, you might have temporary work\-in\-progress folders\. Or you might use a NetApp system and want to exclude NetApp backup folders\. In these cases, you use the following filter\.

`*/.snapshot`

To exclude folders at any level in the file hierarchy, you can create a task to configure an exclude filter like the following\. 

`*/folder-to-exclude-1`\|`*/folder-to-exclude-2`

To exclude folders at the top level of the source location, you can create a task to configure an exclude filter like the following\. 

`/top-level-folder-to-exclude-1`\|`/top-level-folder-to-exclude-2`

**Include a subset of the folders on your source location**  
In some cases, your source location might be a large share, and you need to transfer a subset of the folders under the root\. To include specific folders, start a task execution with an include filter like the following\.

`/folder-to-transfer/*`

**Exclude specific file types**  
To exclude certain file types from the transfer, you can create a task execution with an exclude filter such as `*.temp`\.

**Transfer individual files you specify**  
To transfer a list of individual files, start a task execution with an include filter like the following: "`/folder/subfolder/file1.txt`\|`/folder/subfolder/file2.txt`\|`/folder/subfolder/file2.txt`"