<p align="center">
  <img src="https://github.com/user-attachments/assets/b44a514e-0a41-4f09-8786-fc529ed51cf9" alt="Splitwise clone Banner"/>
</p>

# **📄 SplitWise Clone Installation Guide**

### 📚 **Table of Contents**

1. [📥 Clone the Repository](#-1-clone-the-repository)
2. [📦 Install Dependencies](#-2-install-dependencies)
3. [🎨 Install and Configure Tailwind CSS](#-3-install-and-configure-tailwind-css)
4. [🗄️ Setup Appwrite (Database Configuration)](#-4-setup-appwrite-database-configuration)
   - [🔑 Create an Appwrite Account](#-step-1-create-an-appwrite-account)
   - [📁 Create a New Project](#-step-2-create-a-new-project)
   - [🛠️ Setup the Database](#-step-3-setup-the-database)
   - [🏗️ Create Collections](#-step-4-create-collections)
   - [🔒 Update Collection Permissions](#-step-5-update-collection-permissions)
   - [🔑 Copy IDs to .env File](#-step-6-copy-ids-to-env-file)
5. [🚀 Run the Project](#-5-run-the-project)
6. [🌐 Deploy on Vercel](#-6-deploy-on-vercel)
   - [🔌 Configure Appwrite Integration](#-configure-appwrite-integration)
7. [📧 Need Help?](#-need-help)
8. [🎥 Appwrite Database Guide Video](#-appwrite-database-guide-video)
9. [📑 Documentation](#-documentation)
   - [📂 Google Drive](#google-drive)
   - [📄 DOC PDF](#doc-pdf)
10. [📊 Database Design](#-database-design)
11. [🔄 Flowchart](#-flowchart)
12. [💸 Simplify Debt Flowchart](#-simplify-debt-flowchart)

---

### 📥 **1. Clone the Repository**

Begin by cloning the SplitWise repository to your local machine


### 📦 **2. Install Dependencies**

Navigate to the project directory and install the required Node.js packages:

```bash
cd splitwise
npm install
```

### 🎨 **3. Install and Configure Tailwind CSS**

Install Tailwind CSS and initialize it in your project:

```bash
npm install -D tailwindcss
npx tailwindcss init
```

---

### 🗄️ **4. Setup Appwrite (Database Configuration)**

#### 🚀 **Quick Option: Import My Database Setup (Migration)**

**Skip the manual steps below and directly migrate my database configuration and data!**

1. Create a new project in Appwrite.
2. Go to **Settings** → **Migrations** → **Import Project Data**.
3. Use the following required details:
   - **Endpoint**
   - **Project ID**
   - **API Key**

---

#### 🛠️ **Manual Option: Create the Database Yourself**

If you prefer to set up the database manually, follow these steps:

#### 🔑 **Step 1: Create an Appwrite Account**

- Sign up for an Appwrite account at [Appwrite](https://appwrite.io).

#### 📁 **Step 2: Create a New Project**

- In the Appwrite dashboard, create a new project (e.g., **Splitwise**).

#### 🛠️ **Step 3: Setup the Database**

- Go to the **Databases** section and create a new database (e.g., **Expense**).

#### 🏗️ **Step 4: Create Collections**

- Create the following collections and there attributes within your database:

⚠️ **Warning**: Ensure that you use the attribute names and related collections exactly as mentioned below. To avoid errors, **copy and paste the names directly** where applicable.

1. **Users**

   - **UserName**: `string` (Default: `-`)
   - **name**: `string` (Default: `-`)
   - **email**: `email` (Default: `-`)
   - **accountId**: `string` (Default: `-`)

2. **Groups**

   - **groupName**: `string` (Default: `-`)
   - **Creator**: `Relationship` (Two-way Relationship with `Users`; `Many to one`,
     Attribute Key (related collection): `groups`, Cascade on delete)
   - **Members**: `Relationship` (Two-way Relationship with **Users**; `Many to Many`,
     Attribute Key (related collection): `UserMember`, Set Null on delete)

3. **Friends**

   - **friendsId**: `Relationship` (Two-way Relationship with **Users**; `Many to many`,
     Attribute Key (related collection): `friendCollection`, Set Null on delete)
   - **CollectionId**: `Relationship` (Two-way Relationship with **Users**; `Many to one`,
     Attribute Key (related collection): `List`, Set Null on delete)

4. **Activity**

   - **Desc**: `string` (Default: `-`)
   - **Time**: `DateTime` (Default: `-`)
   - **Amout**: `string` (Default: `-`) _Note: If you change this spelling (Amout), update it in the React app._
   - **IsSettled**: `boolean` (Default: `false`)
   - **splitMember**: `Relationship` (Two-way Relationship with **Users**; `Many to many`,
     Attribute Key (related collection): `members`, Set Null on delete)
   - **PaidBy**: `Relationship` (Two-way Relationship with **Users**; `Many to one`,
     Attribute Key (related collection): `activity`, Set Null on delete)
   - **Group**: `Relationship` (Two-way Relationship with **Groups**; `Many to one`,
     Attribute Key (related collection): `activity`, Cascade on delete)

5. **Transaction**
   - **Amount**: `string` (Default: `-`)
   - **Time**: `DateTime` (Default: `-`)
   - **IsOld**: `boolean` (Default: `false`)
   - **payerId**: `Relationship` (Two-way Relationship with **Users**; `Many to one`,
     Attribute Key (related collection): `transaction`, Set Null on delete)
   - **receiverId**: `Relationship` (Two-way Relationship with **Users**; `Many to one`,
     Attribute Key (related collection): `transactionId`, Set Null on delete)

#### 🔒 **Step 5: Update Collection Permissions**

1. **Navigate to Collection Settings**:

   - In your **Appwrite** dashboard, open the **Collection Settings** for each collection that requires permission changes.

2. **Modify Permissions**:

   - For each collection, go to the **Settings** tab.
   - Under the **Permissions** section, update the role to `Any`.
   - Ensure that the following permissions are checked:
     - **Create**
     - **Read**
     - **Update**
     - **Delete**

3. **Save Changes**:
   - Repeat the process for each collection, ensuring the correct permissions are applied.

---

#### 🔑 **Step 6: Copy IDs to .env File**

1. In **Project Settings**, copy the **Project ID** and **API Endpoint**.
2. Copy the **Database ID** and all **Collection IDs** from the database.
3. Create a `.env.local` file and add the copied IDs as follows:
4. Now no need of `.env.sample`

#### **Sample .env.local File**

```bash
VITE_APPWRITE_URL='https://cloud.appwrite.io/v1'
VITE_APPWRITE_PROJECT_ID='67c067565211fbcf173'
VITE_APPWRITE_DATABASE_ID='657c0953b37f27853d8'
VITE_APPWRITE_USER_COLLECTION_ID='657casd56db7f49cee3b20'
VITE_APPWRITE_GROUPS_COLLECTION_ID='657c09839424664asd87496'
VITE_APPWRITE_ACTIVITY_COLLECTION_ID='657c099dd2eda1ddebb'
VITE_APPWRITE_FRIENDS_COLLECTION_ID='681b28b356casds5dd28d'
VITE_APPWRITE_TRANSACTION_COLLECTION_ID='65aasd54f3a07aec3c8'
```

---

### 🚀 **5. Run the Project**

Finally, start the development server:

```bash
npm run dev
```

---

### 🌐 **6. Deploy on Vercel**

1. **Deploy on Vercel**:

   - Go to [Vercel](https://vercel.com/) and sign in or sign up.
   - Connect your **GitHub** account and select the Git repository of the project you want to deploy.
   - Follow the prompts to deploy your project. Vercel will handle the deployment and provide you with a live URL once completed.
   - Add .env.local in Vercel Spliwise Project Go in Settings Environment Variables And Paste Your all  .env.local in that

2. **Configure Appwrite Integration**:
   - After deployment, copy the Vercel deployment URL (e.g., `https://your-project-name.vercel.app`).
   - Log in to your **Appwrite** dashboard.
   - Go to your **Project Overview** and scroll down to the **Integrations** section.
   - Click **Add Platform** and select `Web App`.
   - In the `Name` field, paste your Vercel deployment URL, and in the `Hostname` field, enter `*.vercel.app`.
3. **Complete Setup**:
   - Skip any additional configurations unless required by your project setup.
   - Your app is now deployed and integrated with Appwrite! 🎉

---


### Built With

React - A JavaScript library for building user interfaces.
React Router - Declarative routing for React.js.
Tailwind CSS - A utility-first CSS framework.

# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.


## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
export default {
  // other rules...
  parserOptions: {
    ecmaVersion: "latest",
    sourceType: "module",
    project: ["./tsconfig.json", "./tsconfig.node.json"],
    tsconfigRootDir: __dirname,
  },
};
```

- Replace `plugin:@typescript-eslint/recommended` to `plugin:@typescript-eslint/recommended-type-checked` or `plugin:@typescript-eslint/strict-type-checked`
- Optionally add `plugin:@typescript-eslint/stylistic-type-checked`
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and add `plugin:react/recommended` & `plugin:react/jsx-runtime` to the `extends` list
