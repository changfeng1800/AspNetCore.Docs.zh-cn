---
title: 使用 ASP.NET Core 和 MongoDB 构建 Web API
author: prkhandelwal
description: 本教程演示如何使用 MongoDB NoSQL 数据库构建 ASP.NET Core Web API。
ms.author: scaddie
ms.custom: mvc,seodec18
ms.date: 11/29/2018
uid: tutorials/first-mongo-app
ms.openlocfilehash: df3b8656618c813838d6618efc9394f0ccb6e563
ms.sourcegitcommit: 49faca2644590fc081d86db46ea5e29edfc28b7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2018
ms.locfileid: "53121474"
---
# <a name="create-a-web-api-with-aspnet-core-and-mongodb"></a><span data-ttu-id="1ac31-103">使用 ASP.NET Core 和 MongoDB 创建 Web API</span><span class="sxs-lookup"><span data-stu-id="1ac31-103">Create a web API with ASP.NET Core and MongoDB</span></span>

<span data-ttu-id="1ac31-104">作者 [Pratik Khandelwal](https://twitter.com/K2Prk) 和 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="1ac31-104">By [Pratik Khandelwal](https://twitter.com/K2Prk) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="1ac31-105">本教程创建对 [MongoDB](https://www.mongodb.com/what-is-mongodb) NoSQL 数据库执行创建、读取、更新和删除 (CRUD) 操作的 Web API。</span><span class="sxs-lookup"><span data-stu-id="1ac31-105">This tutorial creates a web API that performs Create, Read, Update, and Delete (CRUD) operations on a [MongoDB](https://www.mongodb.com/what-is-mongodb) NoSQL database.</span></span>

<span data-ttu-id="1ac31-106">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="1ac31-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ac31-107">配置 MongoDB</span><span class="sxs-lookup"><span data-stu-id="1ac31-107">Configure MongoDB</span></span>
> * <span data-ttu-id="1ac31-108">创建 MongoDB 数据库</span><span class="sxs-lookup"><span data-stu-id="1ac31-108">Create a MongoDB database</span></span>
> * <span data-ttu-id="1ac31-109">定义 MongoDB 集合和架构</span><span class="sxs-lookup"><span data-stu-id="1ac31-109">Define a MongoDB collection and schema</span></span>
> * <span data-ttu-id="1ac31-110">从 Web API 执行 MongoDB CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="1ac31-110">Perform MongoDB CRUD operations from a web API</span></span>

<span data-ttu-id="1ac31-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-mongo-app/sample)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="1ac31-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-mongo-app/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ac31-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="1ac31-112">Prerequisites</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1ac31-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ac31-113">Visual Studio</span></span>](#tab/visual-studio)

* [<span data-ttu-id="1ac31-114">.NET Core SDK 2.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="1ac31-114">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download/all)
* <span data-ttu-id="1ac31-115">已安装“ASP.NET 和 Web 开发”工作负载的 [Visual Studio 2017 版本 15.9 或更高版本](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1ac31-115">[Visual Studio 2017 version 15.9 or later](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="1ac31-116">MongoDB</span><span class="sxs-lookup"><span data-stu-id="1ac31-116">MongoDB</span></span>](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="1ac31-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1ac31-117">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="1ac31-118">.NET Core SDK 2.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="1ac31-118">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="1ac31-119">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1ac31-119">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="1ac31-120">用于 Visual Studio Code 的 C#</span><span class="sxs-lookup"><span data-stu-id="1ac31-120">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [<span data-ttu-id="1ac31-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="1ac31-121">MongoDB</span></span>](https://docs.mongodb.com/manual/administration/install-community/)

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="1ac31-122">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="1ac31-122">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* [<span data-ttu-id="1ac31-123">.NET Core SDK 2.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="1ac31-123">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="1ac31-124">Visual Studio for Mac 版本 7.7 或更高版本</span><span class="sxs-lookup"><span data-stu-id="1ac31-124">Visual Studio for Mac version 7.7 or later</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="1ac31-125">MongoDB</span><span class="sxs-lookup"><span data-stu-id="1ac31-125">MongoDB</span></span>](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

---

## <a name="configure-mongodb"></a><span data-ttu-id="1ac31-126">配置 MongoDB</span><span class="sxs-lookup"><span data-stu-id="1ac31-126">Configure MongoDB</span></span>

<span data-ttu-id="1ac31-127">如果使用的是 Windows，MongoDB 将默认安装在 C:\Program Files\MongoDB 中。</span><span class="sxs-lookup"><span data-stu-id="1ac31-127">If using Windows, MongoDB is installed at *C:\Program Files\MongoDB* by default.</span></span> <span data-ttu-id="1ac31-128">将 C:\Program Files\MongoDB\Server\<version_number>\bin 添加到 `Path` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="1ac31-128">Add *C:\Program Files\MongoDB\Server\<version_number>\bin* to the `Path` environment variable.</span></span> <span data-ttu-id="1ac31-129">通过此更改可以从开发计算机上的任意位置访问 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="1ac31-129">This change enables MongoDB access from anywhere on your development machine.</span></span>

<span data-ttu-id="1ac31-130">使用以下步骤中的 mongo Shell 可以创建数据库、创建集合和存储文档。</span><span class="sxs-lookup"><span data-stu-id="1ac31-130">Use the mongo Shell in the following steps to create a database, make collections, and store documents.</span></span> <span data-ttu-id="1ac31-131">有关 mongo Shell 命令的详细信息，请参阅[使用 mongo Shell](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell)。</span><span class="sxs-lookup"><span data-stu-id="1ac31-131">For more information on mongo Shell commands, see [Working with the mongo Shell](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell).</span></span>

1. <span data-ttu-id="1ac31-132">选择开发计算机上用于存储数据的目录。</span><span class="sxs-lookup"><span data-stu-id="1ac31-132">Choose a directory on your development machine for storing the data.</span></span> <span data-ttu-id="1ac31-133">例如，在 Windows 上为 *C:\BooksData*。</span><span class="sxs-lookup"><span data-stu-id="1ac31-133">For example, *C:\BooksData* on Windows.</span></span> <span data-ttu-id="1ac31-134">创建目录（如果不存在）。</span><span class="sxs-lookup"><span data-stu-id="1ac31-134">Create the directory if it doesn't exist.</span></span> <span data-ttu-id="1ac31-135">mongo Shell 不会创建新目录。</span><span class="sxs-lookup"><span data-stu-id="1ac31-135">The mongo Shell doesn't create new directories.</span></span>
1. <span data-ttu-id="1ac31-136">打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="1ac31-136">Open a command shell.</span></span> <span data-ttu-id="1ac31-137">运行以下命令以连接到默认端口 27017 上的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="1ac31-137">Run the following command to connect to MongoDB on default port 27017.</span></span> <span data-ttu-id="1ac31-138">请记得将 `<data_directory_path>` 替换为上一步中选择的目录。</span><span class="sxs-lookup"><span data-stu-id="1ac31-138">Remember to replace `<data_directory_path>` with the directory you chose in the previous step.</span></span>

    ```console
    mongod --dbpath <data_directory_path>
    ```

1. <span data-ttu-id="1ac31-139">打开另一个命令行界面实例。</span><span class="sxs-lookup"><span data-stu-id="1ac31-139">Open another command shell instance.</span></span> <span data-ttu-id="1ac31-140">通过运行以下命令来连接到默认测试数据库：</span><span class="sxs-lookup"><span data-stu-id="1ac31-140">Connect to the default test database by running the following command:</span></span>

    ```console
    mongo
    ```

1. <span data-ttu-id="1ac31-141">在命令行界面中运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="1ac31-141">Run the following in a command shell:</span></span>

    ```console
    use BookstoreDb
    ```

    <span data-ttu-id="1ac31-142">如果该命令尚不存在，则将创建名为 BookstoreDb 的数据库。</span><span class="sxs-lookup"><span data-stu-id="1ac31-142">If it doesn't already exist, a database named *BookstoreDb* is created.</span></span> <span data-ttu-id="1ac31-143">如果该数据库存在，则将为事务打开其连接。</span><span class="sxs-lookup"><span data-stu-id="1ac31-143">If the database does exist, its connection is opened for transactions.</span></span>

1. <span data-ttu-id="1ac31-144">使用以下命令创建 `Books` 集合：</span><span class="sxs-lookup"><span data-stu-id="1ac31-144">Create a `Books` collection using following command:</span></span>

    ```console
    db.createCollection('Books')
    ```

    <span data-ttu-id="1ac31-145">显示以下结果：</span><span class="sxs-lookup"><span data-stu-id="1ac31-145">The following result is displayed:</span></span>

    ```console
    { "ok" : 1 }
    ```

1. <span data-ttu-id="1ac31-146">使用以下命令定义 `Books` 集合的架构并插入两个文档：</span><span class="sxs-lookup"><span data-stu-id="1ac31-146">Define a schema for the `Books` collection and insert two documents using the following command:</span></span>

    ```console
    db.Books.insertMany([{'Name':'Design Patterns','Price':54.93,'Category':'Computers','Author':'Ralph Johnson'}, {'Name':'Clean Code','Price':43.15,'Category':'Computers','Author':'Robert C. Martin'}])
    ```

    <span data-ttu-id="1ac31-147">显示以下结果：</span><span class="sxs-lookup"><span data-stu-id="1ac31-147">The following result is displayed:</span></span>

    ```console
    {
      "acknowledged" : true,
      "insertedIds" : [
        ObjectId("5bfd996f7b8e48dc15ff215d"),
        ObjectId("5bfd996f7b8e48dc15ff215e")
      ]
    }
    ```

1. <span data-ttu-id="1ac31-148">使用以下命令查看数据库中的文档：</span><span class="sxs-lookup"><span data-stu-id="1ac31-148">View the documents in the database using the following command:</span></span>

    ```console
    db.Books.find({}).pretty()
    ```

    <span data-ttu-id="1ac31-149">显示以下结果：</span><span class="sxs-lookup"><span data-stu-id="1ac31-149">The following result is displayed:</span></span>

    ```console
    {
      "_id" : ObjectId("5bfd996f7b8e48dc15ff215d"),
      "Name" : "Design Patterns",
      "Price" : 54.93,
      "Category" : "Computers",
      "Author" : "Ralph Johnson"
    }
    {
      "_id" : ObjectId("5bfd996f7b8e48dc15ff215e"),
      "Name" : "Clean Code",
      "Price" : 43.15,
      "Category" : "Computers",
      "Author" : "Robert C. Martin"
    }
    ```

    <span data-ttu-id="1ac31-150">该架构将为每个文档添加类型 `ObjectId` 的自动生成的 `_id` 属性。</span><span class="sxs-lookup"><span data-stu-id="1ac31-150">The schema adds an autogenerated `_id` property of type `ObjectId` for each document.</span></span>

<span data-ttu-id="1ac31-151">数据库可供使用了。</span><span class="sxs-lookup"><span data-stu-id="1ac31-151">The database is ready.</span></span> <span data-ttu-id="1ac31-152">你可以开始创建 ASP.NET Core Web API。</span><span class="sxs-lookup"><span data-stu-id="1ac31-152">You can start creating the ASP.NET Core web API.</span></span>

## <a name="create-the-aspnet-core-web-api-project"></a><span data-ttu-id="1ac31-153">创建 ASP.NET Core Web API 项目</span><span class="sxs-lookup"><span data-stu-id="1ac31-153">Create the ASP.NET Core web API project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1ac31-154">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ac31-154">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="1ac31-155">转到“文件” > “新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-155">Go to **File** > **New** > **Project**.</span></span>
1. <span data-ttu-id="1ac31-156">选择“ASP.NET Core Web 应用程序”，将项目命名为“BooksApi”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-156">Select **ASP.NET Core Web Application**, name the project *BooksApi*, and click **OK**.</span></span>
1. <span data-ttu-id="1ac31-157">选择“.NET Core”目标框架和“ASP.NET Core 2.1”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-157">Select the **.NET Core** target framework and **ASP.NET Core 2.1**.</span></span> <span data-ttu-id="1ac31-158">选择“API”项目模板，然后单击“确定”：</span><span class="sxs-lookup"><span data-stu-id="1ac31-158">Select the **API** project template, and click **OK**:</span></span>
1. <span data-ttu-id="1ac31-159">在“包管理器控制台”窗口中，导航到项目根。</span><span class="sxs-lookup"><span data-stu-id="1ac31-159">In the **Package Manager Console** window, navigate to the project root.</span></span> <span data-ttu-id="1ac31-160">运行以下命令以安装适用于 MongoDB 的 .NET 驱动程序：</span><span class="sxs-lookup"><span data-stu-id="1ac31-160">Run the following command to install the .NET driver for MongoDB:</span></span>

    ```powershell
    Install-Package MongoDB.Driver -Version 2.7.2
    ```

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="1ac31-161">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1ac31-161">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="1ac31-162">在命令行界面中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="1ac31-162">Run the following commands in a command shell:</span></span>

    ```console
    dotnet new webapi -o BooksApi
    code BooksApi
    ```

    <span data-ttu-id="1ac31-163">将在 Visual Studio Code 中生成并打开以 .NET Core 为目标的新 ASP.NET Core Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="1ac31-163">A new ASP.NET Core web API project targeting .NET Core is generated and opened in Visual Studio Code.</span></span>

1. <span data-ttu-id="1ac31-164">显示“'BooksApi' 中缺少进行生成和调试所需的资产。是否添加它们?”通知时，单击“是”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-164">Click **Yes** when the *Required assets to build and debug are missing from 'BooksApi'. Add them?* notification appears.</span></span>
1. <span data-ttu-id="1ac31-165">打开“集成终端”并导航到项目根。</span><span class="sxs-lookup"><span data-stu-id="1ac31-165">Open **Integrated Terminal** and navigate to the project root.</span></span> <span data-ttu-id="1ac31-166">运行以下命令以安装适用于 MongoDB 的 .NET 驱动程序：</span><span class="sxs-lookup"><span data-stu-id="1ac31-166">Run the following command to install the .NET driver for MongoDB:</span></span>

    ```console
    dotnet add BooksApi.csproj package MongoDB.Driver -v 2.7.2
    ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="1ac31-167">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="1ac31-167">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

1. <span data-ttu-id="1ac31-168">转到“文件” > “新建解决方案” > “.NET Core” > “应用”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-168">Go to **File** > **New Solution** > **.NET Core** > **App**.</span></span>
1. <span data-ttu-id="1ac31-169">选择“ASP.NET Core Web API”C# 项目模板，然后单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-169">Select the **ASP.NET Core Web API** C# project template, and click **Next**.</span></span>
1. <span data-ttu-id="1ac31-170">从“目标框架”下拉列表中选择“.NET Core 2.2”，然后单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-170">Select **.NET Core 2.2** from the **Target Framework** drop-down list, and click **Next**.</span></span>
1. <span data-ttu-id="1ac31-171">输入“BooksApi”作为“项目名称”，然后单击“创建”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-171">Enter *BooksApi* for the **Project Name**, and click **Create**.</span></span>
1. <span data-ttu-id="1ac31-172">在“解决方案”面板中，右键单击项目的“依赖项”节点，然后选择“添加包”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-172">In the **Solution** pad, right-click the project's **Dependencies** node and select **Add Packages**.</span></span>
1. <span data-ttu-id="1ac31-173">在搜索框中输入“MongoDB.Driver”，选择“MongoDB.Driver”包，然后单击“添加包”。</span><span class="sxs-lookup"><span data-stu-id="1ac31-173">Enter *MongoDB.Driver* in the search box, select the *MongoDB.Driver* package, and click **Add Package**.</span></span>
1. <span data-ttu-id="1ac31-174">在“许可证接受”对话框中单击“接受”按钮。</span><span class="sxs-lookup"><span data-stu-id="1ac31-174">Click the **Accept** button in the **License Acceptance** dialog.</span></span>

---

## <a name="add-a-model"></a><span data-ttu-id="1ac31-175">添加模型</span><span class="sxs-lookup"><span data-stu-id="1ac31-175">Add a model</span></span>

1. <span data-ttu-id="1ac31-176">将 Models 目录添加到项目根。</span><span class="sxs-lookup"><span data-stu-id="1ac31-176">Add a *Models* directory to the project root.</span></span>
1. <span data-ttu-id="1ac31-177">使用以下代码将 `Book` 类添加到 Models 目录：</span><span class="sxs-lookup"><span data-stu-id="1ac31-177">Add a `Book` class to the *Models* directory with the following code:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Models/Book.cs)]

<span data-ttu-id="1ac31-178">在前面的类中，将公共语言运行时 (CLR) 对象映射到 MongoDB 集合时需要 `Id` 属性。</span><span class="sxs-lookup"><span data-stu-id="1ac31-178">In the preceding class, the `Id` property is required for mapping the Common Language Runtime (CLR) object to the MongoDB collection.</span></span> <span data-ttu-id="1ac31-179">类中的其他属性使用 `[BsonElement]` 属性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="1ac31-179">Other properties in the class are decorated with the `[BsonElement]` attribute.</span></span> <span data-ttu-id="1ac31-180">该属性的值表示 MongoDB 集合中的属性名称。</span><span class="sxs-lookup"><span data-stu-id="1ac31-180">The attribute's value represents the property name in the MongoDB collection.</span></span>

## <a name="add-a-crud-operations-class"></a><span data-ttu-id="1ac31-181">添加 CRUD 操作类</span><span class="sxs-lookup"><span data-stu-id="1ac31-181">Add a CRUD operations class</span></span>

1. <span data-ttu-id="1ac31-182">将 Services 目录添加到项目根。</span><span class="sxs-lookup"><span data-stu-id="1ac31-182">Add a *Services* directory to the project root.</span></span>
1. <span data-ttu-id="1ac31-183">使用以下代码将 `BookService` 类添加到 Services 目录：</span><span class="sxs-lookup"><span data-stu-id="1ac31-183">Add a `BookService` class to the *Services* directory with the following code:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Services/BookService.cs?name=snippet_BookServiceClass)]

1. <span data-ttu-id="1ac31-184">将 MongoDB 连接字符串添加到 appsettings.json：</span><span class="sxs-lookup"><span data-stu-id="1ac31-184">Add the MongoDB connection string to *appsettings.json*:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/appsettings.json?highlight=2-4)]

    <span data-ttu-id="1ac31-185">将在 `BookService` 类构造函数中访问前面的 `BookstoreDb` 属性。</span><span class="sxs-lookup"><span data-stu-id="1ac31-185">The preceding `BookstoreDb` property is accessed in the `BookService` class constructor.</span></span>

1. <span data-ttu-id="1ac31-186">在 `Startup.ConfigureServices` 中，向依赖关系注入系统注册 `BookService` 类：</span><span class="sxs-lookup"><span data-stu-id="1ac31-186">In `Startup.ConfigureServices`, register the `BookService` class with the Dependency Injection system:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Startup.cs?name=snippet_ConfigureServices&highlight=3)]

    <span data-ttu-id="1ac31-187">必须执行前面的服务注册才能支持消费类中的构造函数注入。</span><span class="sxs-lookup"><span data-stu-id="1ac31-187">The preceding service registration is necessary to support constructor injection in consuming classes.</span></span>

<span data-ttu-id="1ac31-188">`BookService` 类使用以下 `MongoDB.Driver` 成员对数据库执行 CRUD 操作：</span><span class="sxs-lookup"><span data-stu-id="1ac31-188">The `BookService` class uses the following `MongoDB.Driver` members to perform CRUD operations against the database:</span></span>

* <span data-ttu-id="1ac31-189">`MongoClient` &ndash; 读取执行数据库操作的服务器实例。</span><span class="sxs-lookup"><span data-stu-id="1ac31-189">`MongoClient` &ndash; Reads the server instance for performing database operations.</span></span> <span data-ttu-id="1ac31-190">此类的构造函数提供了 MongoDB 连接字符串：</span><span class="sxs-lookup"><span data-stu-id="1ac31-190">The constructor of this class is provided the MongoDB connection string:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Services/BookService.cs?name=snippet_BookServiceConstructor&highlight=3)]

* <span data-ttu-id="1ac31-191">`IMongoDatabase` &ndash; 表示用于执行操作的 Mongo 数据库。</span><span class="sxs-lookup"><span data-stu-id="1ac31-191">`IMongoDatabase` &ndash; Represents the Mongo database for performing operations.</span></span> <span data-ttu-id="1ac31-192">本教程在界面上使用泛型 `GetCollection<T>(collection)` 方法来获取对特定集合中的数据的访问。</span><span class="sxs-lookup"><span data-stu-id="1ac31-192">This tutorial uses the generic `GetCollection<T>(collection)` method on the interface to gain access to data in a specific collection.</span></span> <span data-ttu-id="1ac31-193">调用此方法后，可以对集合执行 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="1ac31-193">CRUD operations can be performed against the collection after this method is called.</span></span> <span data-ttu-id="1ac31-194">在 `GetCollection<T>(collection)` 方法调用中：</span><span class="sxs-lookup"><span data-stu-id="1ac31-194">In the `GetCollection<T>(collection)` method call:</span></span>
  * <span data-ttu-id="1ac31-195">`collection` 表示集合名称。</span><span class="sxs-lookup"><span data-stu-id="1ac31-195">`collection` represents the collection name.</span></span>
  * <span data-ttu-id="1ac31-196">`T` 表示存储在集合中的 CLR 对象类型。</span><span class="sxs-lookup"><span data-stu-id="1ac31-196">`T` represents the CLR object type stored in the collection.</span></span>

<span data-ttu-id="1ac31-197">`GetCollection<T>(collection)` 返回 `MongoCollection` 对象，该对象表示集合。</span><span class="sxs-lookup"><span data-stu-id="1ac31-197">`GetCollection<T>(collection)` returns a `MongoCollection` object representing the collection.</span></span> <span data-ttu-id="1ac31-198">在本教程中，对集合调用以下方法：</span><span class="sxs-lookup"><span data-stu-id="1ac31-198">In this tutorial, the following methods are invoked on the collection:</span></span>

* <span data-ttu-id="1ac31-199">`Find<T>` &ndash; 返回集合中与提供的搜索条件匹配的所有文档。</span><span class="sxs-lookup"><span data-stu-id="1ac31-199">`Find<T>` &ndash; Returns all documents in the collection matching the provided search criteria.</span></span>
* <span data-ttu-id="1ac31-200">`InsertOne` &ndash; 插入提供的对象作为集合中的新文档。</span><span class="sxs-lookup"><span data-stu-id="1ac31-200">`InsertOne` &ndash; Inserts the provided object as a new document in the collection.</span></span>
* <span data-ttu-id="1ac31-201">`ReplaceOne` &ndash; 将与提供的搜索条件匹配的单个文档替换为提供的对象。</span><span class="sxs-lookup"><span data-stu-id="1ac31-201">`ReplaceOne` &ndash; Replaces the single document matching the provided search criteria with the provided object.</span></span>
* <span data-ttu-id="1ac31-202">`DeleteOne` &ndash; 删除与提供的搜索条件匹配的单个文档。</span><span class="sxs-lookup"><span data-stu-id="1ac31-202">`DeleteOne` &ndash; Deletes a single document matching the provided search criteria.</span></span>

## <a name="add-a-controller"></a><span data-ttu-id="1ac31-203">添加控制器</span><span class="sxs-lookup"><span data-stu-id="1ac31-203">Add a controller</span></span>

1. <span data-ttu-id="1ac31-204">使用以下代码将 `BooksController` 类添加到 Controllers 目录：</span><span class="sxs-lookup"><span data-stu-id="1ac31-204">Add a `BooksController` class to the *Controllers* directory with the following code:</span></span>

    [!code-csharp[](first-mongo-app/sample/BooksApi/Controllers/BooksController.cs)]

    <span data-ttu-id="1ac31-205">前面的 Web API 控制器：</span><span class="sxs-lookup"><span data-stu-id="1ac31-205">The preceding web API controller:</span></span>

    * <span data-ttu-id="1ac31-206">使用 `BookService` 类执行 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="1ac31-206">Uses the `BookService` class to perform CRUD operations.</span></span>
    * <span data-ttu-id="1ac31-207">包含操作方法以支持 GET、POST、PUT 和 DELETE HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="1ac31-207">Contains action methods to support GET, POST, PUT, and DELETE HTTP requests.</span></span>
1. <span data-ttu-id="1ac31-208">生成并运行应用。</span><span class="sxs-lookup"><span data-stu-id="1ac31-208">Build and run the app.</span></span>
1. <span data-ttu-id="1ac31-209">在浏览器中导航到 `http://localhost:<port>/api/books`。</span><span class="sxs-lookup"><span data-stu-id="1ac31-209">Navigate to `http://localhost:<port>/api/books` in your browser.</span></span> <span data-ttu-id="1ac31-210">将显示下面的 JSON 响应：</span><span class="sxs-lookup"><span data-stu-id="1ac31-210">The following JSON response is displayed:</span></span>

    ```json
    [
      {
        "id":"5bfd996f7b8e48dc15ff215d",
        "bookName":"Design Patterns",
        "price":54.93,
        "category":"Computers",
        "author":"Ralph Johnson"
      },
      {
        "id":"5bfd996f7b8e48dc15ff215e",
        "bookName":"Clean Code",
        "price":43.15,
        "category":"Computers",
        "author":"Robert C. Martin"
      }
    ]
    ```

## <a name="next-steps"></a><span data-ttu-id="1ac31-211">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1ac31-211">Next steps</span></span>

<span data-ttu-id="1ac31-212">有关构建 ASP.NET Core Web API 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="1ac31-212">For more information on building ASP.NET Core web APIs, see the following resources:</span></span>

* <xref:web-api/index>
* <xref:web-api/action-return-types>