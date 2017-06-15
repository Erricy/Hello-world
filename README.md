# Hello-world
Just a Repository...

package com.huike.dao;

import java.util.List;

import com.huike.domain.Customer;
import com.huike.utils.JDBCUtils_C3P0;

import java.sql.SQLException;

import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;

public class CustomerDao {
	
	/*
	 * 增加客户
	 */
	public void add(Customer c) {
		
		QueryRunner runner = new QueryRunner(JDBCUtils_C3P0.getDataSource());
		String sql = "insert into t_customer (id,name,birthday,phone,email,gender,preference,type,description) values(?,?,?,?,?,?,?,?,?)";
		Object[] params = {c.getId(),c.getName(),c.getBirthday(),c.getPhone(),c.getEmail(),c.getGender(),c.getPreference(),c.getType(),c.getDescription()};
		try {
			runner.update(sql,params);
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	/*
	 * 删除客户
	 */
	public void delete(String id) {
		
		
		QueryRunner runner = new QueryRunner(JDBCUtils_C3P0.getDataSource());
		String sql = "delete from t_customer where id = ?";
		Object[] params = {id};
		try {
			runner.update(sql,params);
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	/*
	 * 修改客户
	 */
	public void update(Customer c) {
		
		QueryRunner runner = new QueryRunner(JDBCUtils_C3P0.getDataSource());
		String sql = "update t_customer set name = ?,birthday = ?,phone = ?,email = ?,gender = ?,preference = ?,type = ?,description = ? where id = ?";
		Object[] params = {c.getName(),c.getBirthday(),c.getPhone(),c.getEmail(),c.getGender(),c.getPreference(),c.getType(),c.getDescription(),c.getId()};
		try {
			runner.update(sql,params);
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	/*
	 * 
	 * 根据客户的id,查询客户详细信息
	 */
	public Customer find(String id) {
		
		QueryRunner runner = new QueryRunner(JDBCUtils_C3P0.getDataSource());
		String sql = "select id,name,birthday,phone,email,gender,preference,type,description from t_customer where id = ?";
		Object[] params = {id};
		Customer customer = null;
		try {
			customer = (Customer)runner.query(sql,new BeanHandler(Customer.class),params);
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return customer;
		
	}	

	/*
	 * 查询所有的客户
	 */
	public List<Customer> findAll() {
		
		QueryRunner runner = new QueryRunner(JDBCUtils_C3P0.getDataSource());
		String sql = "select id,name,birthday,phone,email,gender,preference,type,description from t_customer";
		List<Customer> list = null;
		try {
			list = (List<Customer>)runner.query(sql,new BeanListHandler(Customer.class));
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return list;
	}
}
