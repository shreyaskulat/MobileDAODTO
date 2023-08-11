# MobileDAODTO
#MobileDAO
package mobileoperations;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class MobileDAO {
    static Connection con = null;
    ArrayList<MobileDTO> list=new ArrayList<>();

    static {
        try {
            con = DriverManager.getConnection("jdbc:mysql://localhost:3306/1eja8", "root", "sql@123");
        } catch (SQLException e) {
            e.printStackTrace();
        }


    }

    public int addMobile(MobileDTO m) {
        PreparedStatement pstmt=null;
        int count=0;
        String query = "insert into mobile values(?,?,?,?,?,?)";
        try {
            pstmt = con.prepareStatement(query);
            pstmt.setInt(1,m.getModelNo());
            pstmt.setString(2,m.getModelName());
            pstmt.setString(3,m.getCompany());
            pstmt.setInt(4,m.getRam());
            pstmt.setInt(5,m.getCamera());
            pstmt.setDouble(6,m.getPrice());
            count=pstmt.executeUpdate();


        } catch (SQLException e) {
            e.printStackTrace();
        }
        return count;

    }

    public ArrayList<MobileDTO> searchMobileByCompany(String name) {
        PreparedStatement pstmt=null;
        ResultSet rs=null;


        String query="select modelname from mobile where company=?";

        try {
            pstmt=con.prepareStatement(query);
            pstmt.setString(1,name);
            rs=pstmt.executeQuery();
            while (rs.next()){
                String modelName=rs.getString(1);

                MobileDTO d2=new MobileDTO();
                d2.setModelName(modelName);
                list.add(d2);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return list;


    }

    public ArrayList<MobileDTO> searchMobileByPrice(double startPrice, double endPrice) {
        Statement stmt=null;
        ResultSet rs=null;


        String query="select * from mobile where price between "+startPrice+" and "+endPrice;

        try {
            stmt=con.createStatement();
            rs=stmt.executeQuery(query);
            while (rs.next()){
                int modelNo=rs.getInt(1);
                String modelName=rs.getString(2);
                String company=rs.getString(3);
                int ram=rs.getInt(4);
                int camera=rs.getInt(5);
                double price=rs.getDouble(6);

                MobileDTO d3=new MobileDTO();
                d3.setModelNo(modelNo);
                d3.setModelName(modelName);
                d3.setCompany(company);
                d3.setRam(ram);
                d3.setCamera(camera);
                d3.setPrice(price);
                list.add(d3);

            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return list;


    }

    public ArrayList<MobileDTO> searchMobileByRam(int ram) {
        Statement stmt=null;
        ResultSet rs=null;

        String query="select * from mobile where ram="+ram+"";

        try {
            stmt=con.createStatement();
            rs=stmt.executeQuery(query);
            while (rs.next()){
                int modelNo=rs.getInt(1);
                String modelName=rs.getString(2);
                String company=rs.getString(3);
                ram = rs.getInt(4);
                int camera=rs.getInt(5);
                double price=rs.getDouble(6);


                MobileDTO d3=new MobileDTO();
                d3.setModelNo(modelNo);
                d3.setModelName(modelName);
                d3.setCompany(company);
                d3.setRam(ram);
                d3.setCamera(camera);
                d3.setPrice(price);
                list.add(d3);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return list;
    }

    public ArrayList<MobileDTO> searchMobileByCamera(double startMP, double endMP) {
        Statement stmt=null;
        ResultSet rs=null;

        String query="select * from mobile where camera between "+startMP+" and "+endMP+"";

        try {
            stmt=con.createStatement();
            rs=stmt.executeQuery(query);
            while (rs.next()){
                int modelNo=rs.getInt(1);
                String modelName=rs.getString(2);
                String company=rs.getString(3);
                int ram=rs.getInt(4);
                int camera=rs.getInt(5);
                double price=rs.getDouble(6);

                MobileDTO d3=new MobileDTO();
                d3.setModelNo(modelNo);
                d3.setModelName(modelName);
                d3.setCompany(company);
                d3.setRam(ram);
                d3.setCamera(camera);
                d3.setPrice(price);
                list.add(d3);

            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return list;

    }

    public int deleteMobile(int modelNo) {
        PreparedStatement pstmt=null;
        int count=0;
        String query="delete from mobile where modelno=?";
        try {
            pstmt=con.prepareStatement(query);
            pstmt.setInt(1,modelNo);
            count=pstmt.executeUpdate();

        } catch (SQLException e) {
            e.printStackTrace();
        }
        return count;

    }

}
#MobileDTO
package mobileoperations;

public class MobileDTO {
    private int modelNo;
    private String modelName;
    private String company;
    private int ram;
    private int camera;
    private double price;

    public MobileDTO() {
        this.modelNo = modelNo;
        this.modelName = modelName;
        this.company = company;
        this.ram = ram;
        this.camera = camera;
        this.price = price;
    }

    public int getModelNo() {
        return modelNo;
    }

    public void setModelNo(int modelNo) {
        this.modelNo = modelNo;
    }

    public String getModelName() {
        return modelName;
    }

    public void setModelName(String modelName) {
        this.modelName = modelName;
    }

    public String getCompany() {
        return company;
    }

    public void setCompany(String company) {
        this.company = company;
    }

    public int getRam() {
        return ram;
    }

    public void setRam(int ram) {
        this.ram = ram;
    }

    public int getCamera() {
        return camera;
    }

    public void setCamera(int camera) {
        this.camera = camera;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public String toString() {

        return modelNo + "\t" + modelName + "\t" + company + "\t" + ram + "\t" + camera + "\t" + price;
    }
}
#MainApp
package mobileoperations;


import java.util.ArrayList;
import java.util.Scanner;

public class MobileMainApp {
    static Scanner sc=new Scanner(System.in);
    public static void main(String[] args) {
        boolean status = true;
        while (status) {
            System.out.println("Select Mode of Operation");
            System.out.println("1: Add Mobile");
            System.out.println("2: Search Mobile");
            System.out.println("3: Delete Mobile");
            int ch = sc.nextInt();
            switch (ch) {
                case 1:
                    addMobile();
                    break;
                case 2:
                    System.out.println("1: Search Mobile By Company");
                    System.out.println("2: Search Mobile By Price");
                    System.out.println("3: Search Mobile By Ram");
                    System.out.println("4: Search Mobile By Camera");
                    int choice = sc.nextInt();
                    if (choice == 1) {
                        searchMobileByCompnay();
                    } else if (choice == 2) {
                        searchMobileByPrice();

                    } else if (choice == 3) {
                        searchMobileByRam();

                    } else if (choice == 4) {
                        searchMobileByCamera();
                    } else {
                        System.out.println("Invalid Choice");
                    }
                    break;
                case 3:
                    deleteMobile();
                    break;
                default:
                    status = false;
            }
        }
    }

    private static void deleteMobile() {
        System.out.println("Enter Model No");
        int modelNo=sc.nextInt();
        MobileDAO d5=new MobileDAO();
        int count=d5.deleteMobile(modelNo);
        System.out.println(count+"RECORD DELETED SUCCESSFULLY");
    }

    private static void searchMobileByCamera() {
        System.out.println("Enter Start MP");
        double startMP= sc.nextDouble();
        System.out.println("Enter End MP");
        double endMP= sc.nextDouble();
        MobileDAO d4=new MobileDAO();
        ArrayList<MobileDTO> mobilelist=d4.searchMobileByCamera(startMP,endMP);
        System.out.println("modelno\tmodelname\tcompany\tram\tcamera\tprice");
        System.out.println("=================================================");
        for (MobileDTO d1:mobilelist){
            System.out.println(d1);
        }
    }

    private static void searchMobileByRam() {
        System.out.println("Select ram");
        System.out.println(2+"GB\t"+4+"GB\t"+6+"GB\t"+8+"GB");
        int ram= sc.nextInt();
        MobileDAO d2=new MobileDAO();
        ArrayList<MobileDTO> mobilelist=d2.searchMobileByRam(ram);
        System.out.println("modelno\tmodelname\tcompany\tram\tcamera\tprice");
        System.out.println("============================================");
        for (MobileDTO dt1:mobilelist){
            System.out.println(dt1);
        }
    }

    private static void searchMobileByPrice() {
        System.out.println("Enter Start Price");
        double startPrice= sc.nextDouble();
        System.out.println("Enter End Price");
        double endPrice= sc.nextDouble();
        MobileDAO d2=new MobileDAO();
        ArrayList<MobileDTO> mobilelist=d2.searchMobileByPrice(startPrice,endPrice);
        System.out.println("modelno\tmodelname\tcompany\tram\tcamera\tprice");
        System.out.println("=================================================");
        for (MobileDTO d:mobilelist){
            System.out.println(d);
        }
    }

    private static void searchMobileByCompnay() {
        System.out.println("Enter Company Name");
        String name=sc.next();

        MobileDAO d1=new MobileDAO();
        ArrayList<MobileDTO> mobilelist =d1.searchMobileByCompany(name);
        System.out.println("modelname");
        System.out.println("============");
        for (MobileDTO d:mobilelist){
            System.out.println(d);
        }
    }

    private static void addMobile() {
        System.out.println("Enter Model No");
        int modelNo= sc.nextInt();
        System.out.println("Enter Model Name");
        String modelName= sc.next();
        System.out.println("Enter Mobile Company");
        String company=sc.next();
        System.out.println("Enter RAM");
        int ram= sc.nextInt();
        System.out.println("Enter Camera");
        int camera= sc.nextInt();
        System.out.println("Enter Mobile Price");
        double price=sc.nextDouble();

        MobileDTO m=new MobileDTO();
        m.setModelNo(modelNo);
        m.setModelName(modelName);
        m.setCompany(company);
        m.setRam(ram);
        m.setCamera(camera);
        m.setPrice(price);

        MobileDAO m1=new MobileDAO();
        int result=m1.addMobile(m);
        System.out.println(result+"MOBILE ADDED SUCCESSFULLY");
    }
}
